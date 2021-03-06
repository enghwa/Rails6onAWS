# Rails6onAWS

Build the Ruby on Rails 6 local development container.
Suggestion: do this in AWS Cloud9. Cloud9 has docker install but you need to install `docker-compose`.
ref: https://docs.docker.com/compose/install/


```
docker build -t ror6dev --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) .

```

## Create a new RoR project - blog
```
docker run -it --user "$(id -u):$(id -g)" -v $PWD:/opt/app ror6dev rails new blog

cp docker-compose.yml blog/
cp Gemfile blog/
cp config/* blog/config
cp env blog/.env

cd blog
export USER_ID=`id -u`
export GROUP_ID=`id -g`
docker-compose run --user "$(id -u):$(id -g)" ror6 rails db:setup
docker-compose up

```
This will mount the `blog` directory inside `ror6dev`. You can use vscode(via remote ssh) or Cloud9 to edit your code.
You can access `ror6` in another shell to run your `rake` or `rails` commands, eg:`rails db:setup`:

```
docker exec -it blog_ror6_1 bash

```
You will need to add your cloud9 to `config/environments/development.rb`.

```
config.hosts << "XXXXXX.amazonaws.com"
```


### Access posgres DB
```
psql -h localhost -U ror6
# pw: mydbpassword
```