# Test 3

Aby zbudować obraz oraz przesłać go do repozytorium DockerHub należy wykorzystać polecenie ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --output type=image,name=docker.io/nikesz/lab4:test3,push=true```.

# Zadanie

Aby postawić kontener z repozytorium obrazów należy wykorzystać polecenie ```docker run -d -p 5000:5000 --restart always --name registry registry:2```.

Aby zbudować obrazu za pomocą Buildkit w taki sposób, że obraz i cache są przesyłane
do lokalnego repozytorium oddzielnie należy wykorzystać polecenie ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --output type=image,name=localhost:5000/localrepository:simplewebapp,push=true --export-cache type=registry,ref=localhost:5000/localrepository:simplewebapp```.

Aby wyczyścić cache należy wykorzystać polecenie ```buildctl prune```.

Aby zbudować obraz wykorzystując zapisane wcześniej dane z budowy obrazu należy wykorzystać polecenie ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --output type=image,name=localhost:5000/localrepository:simplewebapp,push=true --import-cache type=registry,ref=localhost:5000/localrepository:simplewebapp```.

Aby zrealizować analogiczne działanie w oparciu o własne, publiczne repozytorium na DockerHub nalży wykorzystać polecenia ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --output type=image,name=docker.io/nikesz/lab4:simplewebapp,push=true --export-cache type=registry,ref=docker.io/nikesz/lab4:simplewebapp```, ```buildctl prune``` i ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --output type=image,name=docker.io/nikesz/lab4:simplewebapp,push=true --import-cache type=registry,ref=docker.io/nikesz/lab4:simplewebapp```.

# Zadanie dodatkowe

Aby zbudować obrazu za pomocą Buildkit w taki sposób, że cache jest przechowywany lokalnie, a tryb jego eksportowania to max należy wykorzystać polecenie ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --export-cache type=local,dest=.,mode=max```.

Aby wyczyścić cache należy wykorzystać polecenie ```buildctl prune```.

Aby zbudować obraz wykorzystując zapisane wcześniej lokalne dane z budowy obrazu należy wykorzystać polecenie ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --import-cache type=local,src=.```.

Aby zrealizować analogiczne działanie, ale w trybie eksportowania cache min należy wykorzystać polecenia ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --export-cache type=local,dest=.,mode=min```, ```buildctl prune``` i ```buildctl build --ssh default="/home/nikes/.ssh/id_ed25519" --frontend=gateway.v0 --opt source=docker/dockerfile --local context=. --local dockerfile=. --opt filename=./Simpleweb/Dockerfile_test3 --import-cache type=local,src=.```

Tryby eksportowania różnią się tym, iż w trybie min eksportowane są tylko warstwy wynikowego obrazu, natomiast w trybie max wszystkie warstwy z wszystkich etapów pośrednich.