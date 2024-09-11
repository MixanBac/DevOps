Steps:
1) Download Gitlab-Bitnami vm image from https://bitnami.com/stack/gitlab/virtual-machine
2) Upload https://github.com/olindata/sample-gitlabci-cpp-project to your Gitlab server.
3) To unblock SSH https://docs.bitnami.com/virtual-machine/faq/get-started/enable-ssh/
4) https://askubuntu.com/questions/204400/ssh-public-key-no-supported-authentication-methods-available-server-sent-publ
5) Install GitLab Runner using the official GitLab repositories https://docs.gitlab.com/runner/install/linux-repository.html
6) Update /etc/gitlab/gitlab.rb to disable https on gitlab (yes, it is not for production)
- use here your IP, but is must be HTTP
- external_url 'http://192.168.88.228'
- nginx['redirect_http_to_https'] = false
- nginx['ssl_verify_client'] = "off"
7) Reconfigure GitLab for the changes to take effect:
- $ sudo gitlab-ctl reconfigure
8) Register runner. Choose shell executor type. Use your ip and registration-token for command below:
- $ sudo gitlab-runner register --url http://192.168.88.228/ --registration-token yqjsLYNFrbjaC-QhmycE
9) Edit .gitlab-ci.yml to run runner in shell mode (without Docker)
- job:
- script:
- g++ helloworld.cpp -o helloworld
- Run Pipeline: CI/CD > Pipelines > Run pipeline
