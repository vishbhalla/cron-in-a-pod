# Use a full fat linux image:
FROM ubuntu:latest

# Upload our local files to /tmp in the container:
COPY ./echo_env.* /tmp/

# Install cron as it's not installed by the above image as default:
RUN apt-get update && apt upgrade -y && apt-get install -y cron

# Make the cron script executable, and touch the log file it will be writing to:
RUN chmod +x /tmp/echo_env.sh && touch /tmp/cron.log

# Install our cron job in root user's crontab, using the file we copied over above:
RUN crontab -u root /tmp/echo_env.cron

# Start the container by starting the cron service, and spit out the logfile the cron should be writing to:
ENTRYPOINT export -p | grep -v LS_COLORS > /tmp/env.sh && service cron start && tail -f /tmp/cron.log
