include .env
export $(shell sed 's/=.*//' .env)

up:
	sudo docker compose --env-file .env up -d

down:
	sudo docker compose --env-file .env down

restart: down up

logs:
	sudo docker compose --env-file .env logs -f

ps:
	sudo docker compose --env-file .env ps

exec-gitlab:
	sudo docker compose --env-file .env exec gitlab bash

exec-runner:
	sudo docker compose --env-file .env exec gitlab-runner sh

backup:
	sudo docker compose --env-file .env run --rm backup

register-runner:
	sudo docker compose --env-file .env run --rm register-runner

prune:
	sudo docker system prune --volumes --force

clean: down prune

clean -f:
	sudo docker ps -q | xargs -r docker stop && docker ps -a -q | xargs -r docker rm && docker images -q | sort
	-u | xargs -r docker rmi -f && docker volume ls -q | xargs -r docker volume rm && docker builder prune -a -f && docker system prune -a --
	volumes -f

help:
	@echo "Доступные команды:"
	@echo "  up               — Запустить контейнеры"
	@echo "  down             — Остановить контейнеры"
	@echo "  restart          — Перезапустить контейнеры"
	@echo "  logs             — Логирование контейнеров"
	@echo "  ps               — Статус контейнеров"
	@echo "  exec-gitlab      — Войти в контейнер gitlab (bash)"
	@echo "  exec-runner      — Войти в контейнер gitlab-runner (sh)"
	@echo "  backup           — Выполнить резервное копирование вручную"
	@echo "  register-runner  — Зарегистрировать gitlab-runner"
	@echo "  prune            — Очистка dangling images, volumes и т.д."
	@echo "  clean            — Полная остановка и очистка"
