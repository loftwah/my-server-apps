#
# Postfacto, a free, open-source and self-hosted retro tool aimed at helping
# remote teams.
#
# Copyright (C) 2016 - Present Pivotal Software, Inc.
#
# This program is free software: you can redistribute it and/or modify
#
# it under the terms of the GNU Affero General Public License as
#
# published by the Free Software Foundation, either version 3 of the
#
# License, or (at your option) any later version.
#
#
#
# This program is distributed in the hope that it will be useful,
#
# but WITHOUT ANY WARRANTY; without even the implied warranty of
#
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#
# GNU Affero General Public License for more details.
#
#
#
# You should have received a copy of the GNU Affero General Public License
#
# along with this program.  If not, see <https://www.gnu.org/licenses/>.
#

version: '3.8'

services:
  setup:
    image: postfacto/postfacto:${TAG}
    entrypoint: create-admin-user "$ADMIN_EMAIL" "$ADMIN_PASSWORD"
    environment:
      DATABASE_URL: "postgres://postgres:$POSTGRES_PASSWORD@postgres:5432"
      SECRET_KEY_BASE: $SECRET_KEY_BASE
    links:
    - postfacto
    - postgres

  test:
    image: postfacto/smoke:${TAG}
    environment:
      ADMIN_EMAIL: $ADMIN_EMAIL
      ADMIN_PASSWORD: $ADMIN_PASSWORD
      BASE_ADMIN_URL: 'http://postfacto:3000/admin'
      BASE_WEB_URL: 'http://postfacto:3000'
    links:
    - postfacto

  postfacto:
    image: postfacto/postfacto:${TAG}
    ports:
    - '3000:3000'
    environment:
      DATABASE_URL: "postgres://postgres:$POSTGRES_PASSWORD@postgres:5432"
      DISABLE_SSL_REDIRECT: 'true'
      REDIS_URL: 'redis://redis:6379'
      SECRET_KEY_BASE: $SECRET_KEY_BASE
    links:
    - postgres
    - redis

  postgres:
    image: postgres
    environment:
      POSTGRES_PASSWORD: $POSTGRES_PASSWORD

  redis:
    image: redis