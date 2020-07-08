# Vue LearningNote

## Basic


## Debug & Tips

### Get Started

- Force Interrupt using <kbd>Ctrl</kbd>+<kbd>C</kbd>
  Never interrupt your chromedriver installing process. Though it takes time, but once interrupted, you may have to delete all your `node_module` folder and restart once again.

- **`ENOSPC`**, which means 'Error No more hard-disk space available'
  Once a project has mean started defaultly, the maximum watches could be really low, so you should have to enhance the limit by reset `nodemon`'s maximum watches to possible max by using
```shell
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```
as command in the project's root path.
