# heroku-buildpack-mono-apps

Separate apps, buildpacks and procfiles for subdirectories in your monorepo.

### Thanks to

- https://github.com/negativetwelve/heroku-buildpack-subdir
- https://github.com/heroku/heroku-buildpack-multi-procfile

## Example

Example from the command line for monorepo with a `frontend` and `backend` app.

**monorepo/backend** app (python)
1. create the app, add the buildpack, and set the app directory environment variable
   ```bash
   heroku create -a myproject-backend
   heroku buildpacks:add -a myproject-backend https://github.com/AMStrix/heroku-buildpack-mono-apps
   heroku config:set -a myproject-backend HEROKU_APP_DIR=backend
   ```
2. create `Procfile-backend` and `.buildpack-backend` settings files in the root
   ```bash
   printf "web: cd backend && gunicorn my.app:create_app\(\) -b 0.0.0.0:$PORT -w 1" > Procfile-backend
   printf "https://github.com/heroku/heroku-buildpack-python" > .buildpack-backend
   ```
3. deploy
   ```bash
   git push https://git.heroku.com/myproject-backend.git master
   ```

**monorepo/frontend** app (nodejs)
1. create the app, add the buildpack, and set the app directory environment variable
   ```bash
   heroku create -a myproject-frontend
   heroku buildpacks:add -a myproject-frontend https://github.com/AMStrix/heroku-buildpack-mono-apps
   heroku config:set -a myproject-frontend HEROKU_APP_DIR=frontend
   ```
2. create `Procfile-frontend` and `.buildpack-frontend` settings files in the root
   ```bash
   printf "web: cd frontend && yarn start" > Procfile-frontend
   printf "https://github.com/heroku/heroku-buildpack-nodejs" > .buildpack-frontend
   ```
3. deploy
   ```bash
   git push https://git.heroku.com/myproject-frontend.git master
   ```
