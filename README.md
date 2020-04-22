# Rails6onAWS


Build the Ruby on Rails 6 local development container.
Suggestion: do this in AWS Cloud9.

```
docker build -t ror6dev --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) .

```

## Create a new RoR project - blog
```
docker run -it --user "$(id -u):$(id -g)" -v $PWD:/opt/app ror6dev rails new blog

cp Gemfile blog/
cp config/* blog/config
cp env blog/.env
cd blog
docker-compose up

```
This will mount the `blog` directory inside `ror6dev`. You can use vscode(via remote ssh) or Cloud9 to edit your code.
You can access `ror6dev` shell to run your `rake` or `rails` commands, eg:`rails db:setup`:

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