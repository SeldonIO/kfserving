TAG=1.1.0
IMAGE=docker.io/seldonio/alibiexplainer

docker-build-seldon-alibi:
	docker build --file=alibiexplainer.Dockerfile --force-rm=true -t ${IMAGE}:${TAG} .

docker-push-seldon-alibi:
	docker push ${IMAGE}:${TAG}

kind-load-alibi:
	kind load docker-image ${IMAGE}:${TAG}
