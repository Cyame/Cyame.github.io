---
title: Vue Learning Note
date: 2020-07-04 0:00:00
tags: Programming | 编程 | frontend | 前端
---
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

### ESlint

- Sometimes, ESlint could be annoying. The way to shut it down is to change the option of `useEslint` in file `/config/index.js`. But most time, we should initial the grammar check to make sure our codes are under good condition and standard.
