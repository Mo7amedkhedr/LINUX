
# log the uptime every monday on 1:00 pm

crontab -e


0 13 * * 1 uptime >> home/linux/logfile.log
