TAG=1.1.0

ALIBI_IMAGE_NAME_BASE=alibiexplainer
ALIBI_IMAGE=docker.io/seldonio/${ALIBI_IMAGE_NAME_BASE}
ALIBI_IMG_VERSION_REDHAT ?= ${ALIBI_IMAGE_NAME_BASE}-ubi8:${TAG}
ALIBI_IMG_REDHAT ?= seldonio/${ALIBI_IMG_VERSION_REDHAT}


docker-build-seldon-alibi:
	docker build --file=alibiexplainer.Dockerfile --force-rm=true -t ${ALIBI_IMAGE}:${TAG} .

docker-push-seldon-alibi:
	docker push ${ALIBI_IMAGE}:${TAG}

kind-load-alibi:
	kind load docker-image ${ALIBI_IMAGE}:${TAG}

redhat-docker-build-seldon-alibi:
	docker build --file=alibiexplainer.Dockerfile.redhat --force-rm=true -t ${ALIBI_IMG_REDHAT} .

# password can be found at: https://connect.redhat.com/project/3987291/view
redhat-image-scan-alibi:
	docker login -u unused scan.connect.redhat.com
	docker tag ${ALIBI_IMG_REDHAT} scan.connect.redhat.com/ospid-02f3e15b-c16f-4353-affa-61d5f3c6408b/${ALIBI_IMG_VERSION_REDHAT}
	docker push scan.connect.redhat.com/ospid-02f3e15b-c16f-4353-affa-61d5f3c6408b/${ALIBI_IMG_VERSION_REDHAT}


STORAGE_IMAGE_NAME_BASE=storage-initializer
STORAGE_IMAGE=docker.io/seldonio/${STORAGE_IMAGE_NAME_BASE}
STORAGE_IMG_VERSION_REDHAT ?= ${STORAGE_IMAGE_NAME_BASE}-ubi8:${TAG}
STORAGE_IMG_REDHAT ?= seldonio/${STORAGE_IMG_VERSION_REDHAT}


docker-build-seldon-storage:
	docker build --file=storage-initializer.Dockerfile --force-rm=true -t ${STORAGE_IMAGE}:${TAG} .

docker-push-seldon-storage:
	docker push ${STORAGE_IMAGE}:${TAG}

kind-load-storage:
	kind load docker-image ${STORAGE_IMAGE}:${TAG}

redhat-docker-build-seldon-storage:
	docker build --file=storage-initializer.Dockerfile.redhat --force-rm=true -t ${STORAGE_IMG_REDHAT} .

# password can be found at: https://connect.redhat.com/project/3986991/view
redhat-image-scan-storage:
	docker login -u unused scan.connect.redhat.com
	docker tag ${STORAGE_IMG_REDHAT} scan.connect.redhat.com/ospid-dc132f00-5370-46ed-b506-737bb66d3f34/${STORAGE_IMG_VERSION_REDHAT}
	docker push scan.connect.redhat.com/ospid-dc132f00-5370-46ed-b506-737bb66d3f34/${STORAGE_IMG_VERSION_REDHAT}
