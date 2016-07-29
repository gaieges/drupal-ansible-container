# Drupal ansible-container example

> This is intended to be the repo for our [article here](https://tech.napsty.com/2016/06/using-ansible-to-build-and-orchestrate-clean-docker-images.html)

## Intro

This is an example repo to show how to setup and use the great little tool [ansible-container](https://github.com/ansible/ansible-container) to build clean images in your environment.  It's brought to you by the fine folks at [Ansible](http://ansible.com).

## Getting started

### With vagrant

```bash
# bug in xenial makes the 'up' fail, so we provision as well to set it up right
vagrant up ; vagrant provision && vagrant reload  
```

Should get you set up with a working environment to allow you to just jump in and start messing with ansible-container and the drupal install.

### Spinning up this repo in ansible-container

```bash
cd /vagrant
ansible-container build && ansible-container run
```

You'll then need to [run the install script here](http://localhost:8080/drupal-8.1.3/core/install.php).


### Notes

- There are better ways to do this, this was my first attempt at it, and looking back I would start with basic images rather than already customized ones, and just have ansible do all the work.
