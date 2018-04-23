pull:
	docker pull $(IMAGE_NAME)

rm:
	docker rm -f $(CONTAINER_NAME)

remove-image:
	docker rmi -f $(IMAGE_NAME)

kill:
	docker kill $(CONTAINER_NAME)

attach:
	docker exec -ti $(CONTAINER_NAME) /bin/bash

remove-dangling-images:
	docker rmi $(docker images --filter "dangling=true" -q --no-trunc) --force
