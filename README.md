Composer Project Deployment
=========

Deploy a Composer project (including installing dependencies, etc) to a remote server, using a typical "symlink swap" technique. 

Your web server (nginx, apache) should point to `{{ composer_dest }}/{{ composer_live_directory }}` as a starting point. Assuming your project includes a `public` directory, or similar, you will still need to include that in your webserver configuration.

Requirements
------------

Composer must be installed *on the local machine*. The configured repo (and any of its Composer dependencies) must also be reachable *from the local machine*.

Role Variables
--------------

	# Leave these out and force them to be defined in the play?
	composer_repo: git@example.com:Some/Repo.git
	composer_version: master
	composer_dest: /var/www

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
License
-------

MIT
