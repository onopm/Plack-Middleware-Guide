
# Plack::Middleware::AccessLog::Timed

    enable "Plack::Middleware::AccessLog::Timed", 
        format => "%v %h %l %u %t \"%r\" %>s %b %D";


カスタマイズ等は、perldoc Apache::LogFormat::Compiler

- %h $env->{REMOTE_ADDR}
- %u $env->{REMOTE_USER}
- %t $t
- %r $env->{REQUEST_METHOD} $env->{REQUEST_URI} $env->{SERVER_PROTOCOL}
- %s status code
- %b $length
- %T int($reqtime*1_000_000)
- %D $reqtime
- %v $env->{SERVER_NAME}
- %V $env->{HTTP_HOST} || $env->{SERVER_NAME}
- %p $env->{SERVER_PORT}
- %P $$
- %m $env->{REQUEST_METHOD}
- %U $env->{PATH_INFO}
- %q $env->{QUERY_STRING}
- %H $env->{SERVER_PROTOCOL}


