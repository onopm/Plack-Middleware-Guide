
# Devel::NYTProf

普通に使うPlack/PSGI Server@fujiwara より


    use POSIX::AtFork qw/:all/;
    my @opts = qw( addpid=1 start=no sigexit=1
                   forkdepth=0 file=/tmp/nytprof.out );
    $ENV{"NYTPROF"} = join ":", @opts;
    require Devel::NYTProf;
    pthread_atfork( undef, undef,
        sub { 
            DB::enable_profile() if $$ % 11 == 0; 
        },
    );
    builder { 
        ...  
        $app;
    }


