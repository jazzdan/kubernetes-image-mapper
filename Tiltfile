settings = read_json('tilt_option.json', default={})

allow_k8s_contexts(settings.get('allowed_k8s_context'))

default_registry(settings.get('default_registry'))

docker_build("controller:latest", ".", dockerfile='Dockerfile.tilt',
  live_update=[
    sync('.', '/workspace'),
    run('cd /workspace && go mod download', trigger=['go.mod', 'go.sum']),
    run('cd /workspace && GO111MODULE=on go build -o /manager main.go'),
    restart_container(),
  ]
)

k8s_yaml(kustomize('config/default'))
