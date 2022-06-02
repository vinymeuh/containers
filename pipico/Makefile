.DEFAULT_GOAL := help
.PHONY: image container

IMAGE=pipico-alpine
CONTAINER=pipico

image: ## Build image
	podman build -t $(IMAGE) .

container: ## Create container
	podman run -dt --name $(CONTAINER) \
      --volume /home/viny/PodmanVolumes/pipico:/home/viny/pipico:Z,U \
      --group-add keep-groups --volume /dev/bus/usb:/dev/bus/usb \
      localhost/$(IMAGE)

clean: ## Delete container
	podman rm $(CONTAINER)

clean-all: ## Delete container and image
	-podman rm $(CONTAINER)
	podman rmi $(IMAGE)

help: ## Show Help
	@grep -E '^[a-zA-Z0-9_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'
	@exit 0
