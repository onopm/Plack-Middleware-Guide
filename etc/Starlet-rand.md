
# randの初期化問題

普通に使うPlack/PSGI Server@fujiwara より


forkするアプリは、fork後に乱数を初期化するべき。

## Starman

そのままで問題無し

sub child_init_hook {
    my $self = shift;
    srand();
    ...
}

## Starlet

POSIX::AtForkで子プロセス起動時にsrandを設定

use MyApp;
use POSIX::AtFork qw/ pthread_atfork /;
pthread_atfork(undef, undef, sub { 
    open my $fh, '<', '/dev/urandom' or die;
    read($fh, my $seed, 4);
    srand(vec($seed, 0, 32));
});

### fork した後に srand を自動的によぶには

tokuhiromさんのblogより
  http://blog.64p.org/entry/20100819/1282235700

srand() をよんだあとでfork(2) を call した場合、子プロセスと親プロセスでおなじシードをもっているために、複数プロセスで生成される乱数がおなじになってしまうということがある。
この問題に対応するためにはどうしたらいいのかとかんがえていたところ、POSIX::AtFork というモジュールがあったのでこれをつかえばいいということになった。これを利用すると pthread_atfork() に callback を設定できるため、以下のようにして srand() を fork(2) したときに自動的によぶことが可能となる。

use POSIX::AtFork qw/:ALL/;
srand();
POSIX::AtFork->add_to_child(sub { srand(); });
if (my $pid = fork()) {
      say rand();
        waitpid($pid, 0);
} else {
      say rand();
}

