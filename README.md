# log2telegram Docker
<a href="https://hub.docker.com/r/gustaucastells/log2telegram" target="_blank" title="log-to-telegram docker hub">
  <img src="https://img.shields.io/docker/pulls/gustaucastells/log2telegram" alt="Docker Pulls"/>
</a>

A docker container for reading growing log files and sending notifications via the telegram API based on items in a trigger list.

## Setup Docker run
- Copy the `config.yml`

        $ docker run --rm --entrypoint cat gustaucastells/log2telegram  /app/config.yml > config.yml

- Add TelegramBot api and chatID to `config.yml`
- Add triggers to the list to `config.yml`
- Run

        $ docker run -v {location of config.yml}:/app/config.yml -v {location of log file}:/app/file.log dickverbunt/logtotelegram

- Ready! When a line gets added to the log file and matches a trigger it will send this to Telegram.

## Docker compose
- Copy the `config.yml` file

        $ docker run --rm --entrypoint cat gustaucastells/log2telegram  /app/config.yml > config.yml

- Add TelegramBot api and chatID to `config.yml`
- Add triggers to the list to `config.yml`
- Add this to compose.yml
```
log2telegram:
    image: gustaucastells/log2telegram
    container_name: log2telegram
    volumes:
      - /{path-to}/config.yml:/app/config.yml
      - /{path-to-log-file}:/app/file1.log
      - /{path-to-log-file2}:/app/file2.log
      - /{path-to-log-file3}:/app/file3.log
    restart: unless-stopped
```
- Run

        $ docker-compose up -d

- Ready! When a line gets added to the log file and matches one of the triggers in config file it will send the log line to Telegram.

## Notes

- In `config.yml` it's possible to edit the timeout period.
- Logs will be printed to the terminal. There's also a `/app/debug.log` file.

