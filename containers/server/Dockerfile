FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        bash \
        bsdutils \
        less \
        openssh-server \
        procps \
        sudo \
        telnetd \
        update-inetd \
        xinetd \
    && rm -rf /var/lib/apt/lists/*

RUN useradd --create-home --shell /bin/bash alice \
    && echo 'alice:bacon' | chpasswd \
    && mkdir -p /run/sshd /root/.ssh \
    && sed -i 's/^#\?Port .*/Port 2022/' /etc/ssh/sshd_config \
    && printf 'alice ALL=(ALL) /usr/bin/less /home/alice/flag.txt\n' > /etc/sudoers.d/alice-less \
    && chmod 0440 /etc/sudoers.d/alice-less \
    && printf 'placeholder\n' > /home/alice/flag.txt \
    && chown alice:alice /home/alice/flag.txt \
    && chmod 0600 /home/alice/flag.txt \
    && printf 'placeholder\n' > /root/flag.txt \
    && chmod 0600 /root/flag.txt

RUN printf '%s\n' \
    'escape_str() {' \
    '  sed -r '"'"'s/\\/\\\\/g; s/"/\\"/g; s/\a/\\a/g; s/\f/\\f/g; s/\r/\\r/g; s/\t/\\t/g; s/\v/\\v/g'"'"' | tr '"'"'\n'"'"' '"'"'\t'"'"' | sed '"'"'s/\t/\\n/g'"'"' | head -c-2' \
    '}' \
    'log_command() {' \
    '  command=$(fc -ln -1 | sed -r '"'"'s/^[[:blank:]]*//g'"'"' | sed -e '"'"'s/[[:space:]]*$//'"'"' | escape_str)' \
    '  wd=$(realpath "$(pwd)" | escape_str)' \
    '  if [ -n "$command" ]; then' \
    '    logger -p syslog.info --size 8192 -t bash.command "{\"cmd\":\"$command\", \"username\":\"$(echo "$USER" | escape_str)\", \"uid\":\"$UID\",\"wd\":\"$wd\"}"' \
    '  fi' \
    '}' \
    'PS0='"'"'$(log_command)'"'" \
    > /etc/bash.bashrc.docker-logging \
    && printf '\n[ -f /etc/bash.bashrc.docker-logging ] && . /etc/bash.bashrc.docker-logging\n' >> /etc/bash.bashrc

RUN printf '%s\n' \
    'service telnet' \
    '{' \
    '  type        = UNLISTED' \
    '  port        = 22' \
    '  socket_type = stream' \
    '  protocol    = tcp' \
    '  wait        = no' \
    '  user        = root' \
    '  server      = /usr/sbin/in.telnetd' \
    '  disable     = no' \
    '}' > /etc/xinetd.d/telnet

RUN printf '%s\n' \
    '#!/bin/bash' \
    'set -e' \
    'service xinetd start' \
    'exec "$@"' > /usr/local/bin/start-server \
    && chmod 0755 /usr/local/bin/start-server

ENTRYPOINT ["/usr/local/bin/start-server"]
