# Change Log

## [V3.2] - 2023-04-22
 
### Added

- More than 15 **[new variables](https://github.com/HunterXProgrammer/Tasker-mdtest/blob/main/ADVANCED.MD#list-of-tasker-variables)** to play with.

- Support sending Button Messages, List Messages, Poll Messages, Revoke Messages, etc. **[Check here](https://www.reddit.com/r/tasker/comments/12v710y/project_share_whatsapp_advanced_send_messages/)**.

- Support receiving basic Button Response Messages, List Response Messages and Poll Response Messages.
 
## [V3.1] - 2023-03-27
 
### Added

- Automatically reconnect Mdtest on disconnection, due to bad network or WhatsApp Web timeout.

- In case Mdtest is re-connecting due to bad network, messages will wait as long as 40 seconds for Mdtest to acquire `Status: Normal`. You can freely change the time limit in the Task to wait as long as you want.

- Three simple Tasker notifications that show the current status of Mdtest.
  - `Status: Normal` - Mdtest is working properly.
  
  - `Status: Bad Network` - Mdtest is waiting for the network to come back and reconnect .
  
  - `Status: Not Running` - Mdtest is disconnected and not running. It will try to reconnect.
  
  With this, you will no longer need to restart Mdtest yourself. It will all be taken care of by Tasker.
 
### Changed
  
- Replaced the `am` command based communication between Tasker and Mdtest with Tasker's native **Event > File Modified** since `am` had considerable lag on higher Android versions.
 
### Fixed
 
- Fixed some occasional **JSON** parse errors.

- Fixed some `ffmpeg` errors on Samsung.
 
## [V3.0] - 2023-03-20
 
- Initial Release
 
