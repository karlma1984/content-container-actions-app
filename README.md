# Hello world docker action

This action prints "Hello World" to the log or "Hello" + the name of a person to greet. To learn how this action was built, see "[Creating a Docker container action](https://help.github.com/en/articles/creating-a-docker-container-action)" in the GitHub Help documentation.

## Inputs

### `who-to-greet`

**Required** The name of the person to greet. Default `"World"`.

## Outputs

### `time`

The time we greeted you.

## Example usage

```yaml
uses: actions/hello-world-docker-action@master
with:
  who-to-greet: 'Mona the Octocat'
```

# PERSONAL NOTES
Using docker container as an action. Will specify 'docker' and the Dockerfile inside the action.yml spec.

## Some limitation re Dockerfile
- must be run by root
- do not use WORKDIR (which assumed as the root repo folder) - look at the run log to see how --workdir is being passed to docker run
- The entry point in action.yml will override ENTRYPOINT in Dockerfile
- The args in action.yml will override CMD in Dockerfile

## Input / Output
- the args in action.yml will be passed to containers as CMD
- shell script in entry point can get the args as $1, $2, etc
- output values need to be echo'ed to the stdout as 
```
::set-output name=value::
```
look at entrypoint.sh on how it's being echo'ed out