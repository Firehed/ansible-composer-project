Composer Project Deployment
=========

Deploy a Composer project (including installing dependencies, etc) to a remote server, using a typical "symlink swap" technique. 

Your web server (nginx, apache) should point to `{{ composer_dest }}/{{ composer_live_directory }}` as a starting point.
Assuming your project includes a `public` directory, or similar, you will still need to include that in your webserver configuration.

If you need to perform any work on the server before the deployed code goes live, you may provide commands in `composer_pre_link_commands`.
This can be used to warm caches, prepare temp files, etc.
Any commands will be run in the new code's working directory, e.g. `/var/www/releases/20150101000000/`.

Requirements
------------

Composer must be installed *on the local machine*. The configured repo (and any of its Composer dependencies) must also be reachable *from the local machine*.

Role Variables
--------------

	composer_repo: git@example.com:Some/Repo.git
	composer_version: master
	composer_dest: /var/www
	composer_pre_link_commands: []

	composer_www_user: nginx
	composer_www_group: nginx
	
	# These will probably not need to be changed
	composer_release_directory: releases
	composer_live_directory: current

Dependencies
------------

None

Example Playbook
----------------
    - hosts: servers
      roles:
      - role: Firehed.composer-project
        composer_repo: git@github.com:YourUsername/YourWebsite.git
        composer_version: master
        composer_dest: /var/www/yourwebsite
        composer_www_user: nginx
        composer_www_group: nginx
        composer_pre_link_commands:
          - ./vendor/bin/doctrine orm:generate-proxies
License
-------

MIT
