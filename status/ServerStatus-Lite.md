
# Plack::Middleware::ServerStatus::Lite

普通に使うPlack/PSGI Server@fujiwara より

##処理しているworker数を監視

enable "ServerStatus::Lite',
    path         => '/server-status,
    allow        => [ '127.0.0.1' ],
    counter_file => '/tmp/counter_file',
    scoreboard   => '/tmp/score_board';




