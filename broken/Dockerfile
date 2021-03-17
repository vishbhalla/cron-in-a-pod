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

# Start the container spitting out the environment into /tmp/env.sh which the cronjob can use:
ENTRYPOINT service cron start && tail -f /tmp/cron.log
