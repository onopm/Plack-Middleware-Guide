
# Plack::Middleware::Session

## Plack::Session::Store::DBI

Amon2 2.xxのapp.psgiより

    use Plack::Session::Store::DBI;
    use Plack::Session::State::Cookie;
    
    my $db_config = MyApp->config->{DBI} || die "Missing configuration for DBI";
    builder {
        enable 'Plack::Middleware::Session',
            store => Plack::Session::Store::DBI->new(
                get_dbh => sub {
                    DBI->connect( @$db_config ) or die $DBI::errstr;
                }
            ),
            state => Plack::Session::State::Cookie->new(
                httponly => 1,
            );


