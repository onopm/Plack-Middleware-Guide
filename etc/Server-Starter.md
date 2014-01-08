
# Server::Starter

普通に使うPlack/PSGI Server@fujiwara より

##  起動

start_server --port 5000 -- ./app.sh

## app.sh

#!/bin/sh
exec plackup -s Starlet -E production --max_workers 10 app.psgi


max_workersの変更は、app.sh書き換え後に start_serverにHUP



