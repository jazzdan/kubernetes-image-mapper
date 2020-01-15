settings = read_json('tilt_option.json', default={})

allow_k8s_contexts(settings.get('allowed_k8s_context'))

default_registry(settings.get('default_registry'))

docker_build("controller:latest", ".", dockerfile='Dockerfile.tilt',
  live_update=[
    sync('.', '/go/src/github.com/pivotal/kubernetes-image-mapper/'),
    run('CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GO111MODULE=on go build -a -o /manager main.go'),
    restart_container(),
  ]
)

k8s_yaml(kustomize('config/default'))