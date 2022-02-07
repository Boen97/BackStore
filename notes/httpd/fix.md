## httpd not start and cannot see error logs
1. brew info httpd get httpd command path
2. sudo /usr/local/Cellar/httpd/2.4.51/bin/apachectl start could see error logs
3. tail -f /usr/local/var/log/httpd/error_log 查看错误日志，日志的路径可以在https.conf中查看
