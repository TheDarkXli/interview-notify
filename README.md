# interview-notify
Push notifications from IRC for your private tracker interviews

<img src="https://i.imgur.com/ZLFyxgY.png">

## features

this script parses log files from your irc client and attempts to be client-agnostic.

it sends push notifications when:
- interviews are happening
- YOUR interview is happening!
- someone mentions you
- you lose your spot in the queue due to a netsplit
- you get kicked

## installing

- install python3. i suggest homebrew, winget, or just use the installer: https://www.python.org/downloads/
  - _this script might require python3.11_
- install the `requests` module with `pip3 install requests` (or use `pipenv install` to automatically install dependencies)
- clone this repo
  - `git clone https://github.com/ftc2/interview-notify.git`
- `python3 interview_notify.py`

## using

pretty self explanatory if you read the help:

```
./interview_notify.py -h

usage: interview_notify.py [-h] --topic TOPIC [--server SERVER] --log-dir PATH --nick NICK [--check-bot-nicks | --no-check-bot-nicks] [--bot-nicks NICKS] [--mode {red,orp}] [-v] [--version]

IRC Interview Notifier v1.2.10
https://github.com/ftc2/interview-notify

options:
  -h, --help            show this help message and exit
  --topic TOPIC         ntfy topic name to POST notifications to
  --server SERVER       ntfy server to POST notifications to – default: https://ntfy.sh
  --log-dir PATH        path to IRC logs (continuously checks for newest file to parse)
  --nick NICK           your IRC nick
  --check-bot-nicks, --no-check-bot-nicks
                        attempt to parse bot's nick. disable if your log files are not like '<nick> message' – default: enabled
  --bot-nicks NICKS     comma-separated list of bot nicks to watch – default: Gatekeeper
  --mode {red,orp}      interview mode (affects triggers) – default: red
  -v                    verbose (invoke multiple times for more verbosity)
  --version             show program's version number and exit

Sends a push notification with https://ntfy.sh/ when it's your turn to interview.
They have a web client and mobile clients. You can have multiple clients subscribed to this.
Wherever you want notifications: open the client, 'Subscribe to topic', pick a unique topic
  name for this script, and use that everywhere.
On mobile, I suggest enabling the 'Instant delivery' feature as well as 'Keep alerting for
  highest priority'. These will enable fastest and most reliable delivery of the
  notification, and your phone will continuously alarm when your interview is ready.
```

## testing/troubleshooting

first, use `-v` and make sure you can see new messages from IRC showing up:

`interview_notify.py --topic your_topic --log-dir /path/to/logs --nick your_nick -v`

### testing notifications

`interview_notify.py --topic your_topic --log-dir /path/to/logs --nick your_nick --bot-nicks Gatekeeper,your_nick -v`

then type `Currently interviewing: your_nick` in IRC.

if it doesn't work, maybe you have a wonky log file format. try with `--no-check-bot-nicks`:

`interview_notify.py --topic your_topic --log-dir /path/to/logs --nick your_nick --no-check-bot-nicks -v`
