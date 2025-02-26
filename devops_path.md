## v.4 приблизительный план курса:

### план обучения девопс

## 0. devops road map

1. [how browser works](https://github.com/alex/what-happens-when)
1. [how webapps work](https://habr.com/ru/articles/450282/)
1. [Who are devops and SRE](https://www.atlassian.com/devops/frameworks/sre-vs-devops)
1. [DevOps-Roadmap 2025](https://github.com/milanm/DevOps-Roadmap)

## 1. effective shell

1. env setup, .bashrc, aliases, locale, global vars
1. man 1 intro, sections, info, apropos, [File System Hierarchy Standard](https://ru.wikipedia.org/wiki/FHS)
1. asimmetric encryption, ssh key pair, .ssh/config
1. file owners and permissions, sudo, processes and signals
1. std{in,out,err}, redirections, fg, nohup, tmux
1. text, file utils
1. find/xargs, locate, dlocate
1. linux distros, other unicies, deb/rpm/pkg

## 2. git & github

1. регистрация ID, домена, вкл. github pages, hosting, [jekyll](https://github.com/jekyll/jekyll)
1. markdown language, local git, clone, commit, push
1. vscode plugins, [devcontainers](https://code.visualstudio.com/docs/devcontainers/containers)
1. github actions, .workflow
1. [github codespaces](https://docs.github.com/en/codespaces)
1. [coder devpod gitpod codespace comparison](https://www.loft.sh/blog/comparing-coder-vs-codespaces-vs-gitpod-vs-devpod)

## 3. modern web apps and microservices

1. microservices architecture example: [jamstack.com](https://jamstack.com/glossary/)
1. [Awesome Static Website Services](https://github.com/agarrharr/awesome-static-website-services)
1. [12 factor apps](https://12factor.net/)
1. content/design separation: [jekyll resources](https://jekyllrb.com/resources/)
1. [Liquid templating language](https://github.com/Shopify/liquid)
1. add theme and services to your site: ex. comments, analytics, email notifications.
1. github actions workflow
1. [yaml tutorial(rus.)](https://tproger.ru/translations/yaml-za-5-minut-sintaksis-i-osnovnye-vozmozhnosti)
1. [10 шагов к YAML-дзену](https://habr.com/ru/companies/redhatrussia/articles/462125/)


## 4. containers

1. local docker setup, plugins, context, docs
1. docker images, registry, [overlay FS](https://habr.com/ru/companies/skillfactory/articles/547116/)
1. run containers, share folders, inspect, [--format options](https://docs.docker.com/engine/cli/formatting/)
1. [Сборники рецептов jq](https://habr.com/ru/articles/551834/)
1. docker security, check code, build image
1. [docker compose](https://github.com/docker/awesome-compose)
1. [docker swarm cluster](https://docs.docker.com/engine/swarm/)
1. [podman, podman desktop](https://podman-desktop.io/)
1. buildx plugin, buildah tool


## 5. cloud services

1. пройти курс ["Инженер облачных сервисов"](https://practicum.yandex.ru/ycloud/), новые пользователи могут получить грант
1. CDN, WAF for sites, [cloudflare services](https://developers.cloudflare.com/)

## 6. LXC, KVM - personal cloud setup

1. [history of containers](https://www.aquasec.com/blog/a-brief-history-of-containers-from-1970s-chroot-to-docker-2016)
1. [containers intro habr](https://habr.com/ru/articles/541288/)
1. [Containerization vs. Virtualization : understand the differences](https://ubuntu.com/blog/containerization-vs-virtualization)
1. [virtualization software wikipedia](https://en.wikipedia.org/wiki/Comparison_of_platform_virtualization_software)
1. [KVM wiki](https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine)
1. [personal cloud with virt-manager](https://ubuntu.com/server/docs/virtual-machine-manager)
1. [Proxmox VE cluster](https://www.virtualizationhowto.com/category/proxmox/)

## 7. IaaS - terraform, ansible

1. 3 ways to manage infrastructure: manual, imperative via cli tool, declarative via configs
1. [terraform](https://developer.hashicorp.com/terraform)
1. [tf resources](https://github.com/shuaibiyy/awesome-tf)
1. [opentofu tf fork](https://opentofu.org/)
1. [ansible resources](https://github.com/ansible-community/awesome-ansible)

## 8. logging, monitoring, alerts

1. [logs, syslog, rsyslog, systemd-journald](https://habr.com/ru/companies/otus/articles/714266/)
1. [zabbix, icinga, prometheus](https://habr.com/ru/companies/serverspace/articles/705464/)
1. [ELK intro](https://habr.com/ru/articles/671344/)
1. [elastic docs](https://www.elastic.co/docs)
1. [4-golden-signals-demo s-buhar0v](https://www.youtube.com/watch?v=Q_fKb0nrfCg)
1. [grafana: intro to mltp](https://github.com/grafana/intro-to-mltp)

## 9. CI/CD, Gitlab pipelines, Gitea Actions

1. [awesome github actions](https://github.com/sdras/awesome-actions)
1. [gitlab university](https://university.gitlab.com/)
1. [gitlab docs](https://docs.gitlab.com/)

## 10. kubernetes aka k8s, +k3s, +k9s

1. [Marco Luksa "Kubernetes in action"](https://shorturl.at/eokMa)
1. [minimal k3s install](https://k3s.io)
1. [k9s cli](https://github.com/derailed/k9s)
1. [kuber distributions](https://nubenetes.com/matrix-table/)

## 11. openshift aka OKD 

1. [immutable CoreOS for nodes](https://fedoraproject.org/coreos/)
1. [okd.io](https://okd.io/)

## Copiright(C)

Суть проекта - доступность сайта с лекциями и кодом для всех и всегда, из-за отсутствия чего страдают многие курсы. Любой желающий может им пользоваться в любое время, в том числе копировать. Чтобы сохранить авторские права и не создать конкуренцию, материалы сайта доступны под лицензией Creative Commons с ограничениями коммерческого использования [CC BY-NC 4.0 DEED (rus)](https://creativecommons.org/licenses/by-nc/4.0/deed.ru)

###            **[вернуться обратно в блог](index.md)**