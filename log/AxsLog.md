
# Plack::Middleware::AxsLog

普通に使うPlack/PSGI Server@fujiwara より


##100ms以上 or status code [45]xx

    enable "AxsLog',
        ltsv               => 1,
        response_time      => 1,
        long_response_time => 100_000,
        error_only         => 1;




