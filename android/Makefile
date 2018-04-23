PROJECT ?= com.example
PROJECT_TEST ?= $(PROJECT).test

infer-docker:
	clear && \
	docker rm -f $(PROJECT_TEST) || true && \
	docker build --build-arg ANDROID_HOME=${ANDROID_HOME} -t $(PROJECT_TEST) . && \
	docker run -d -e "ANDROID_HOME=${ANDROID_HOME}" -v $$(pwd):/usr/app -v ${ANDROID_HOME}:${ANDROID_HOME} -v ${HOME}/.gradle:/root/.gradle --name $(PROJECT_TEST) -it $(PROJECT_TEST) /bin/bash && \
	docker exec -it $(PROJECT_TEST) script /dev/null -c "infer -- ./gradlew clean build -x validateSigningRelease -x packageRelease -x testRelease -x testDebug -x lint -x pmd"

mobsf:
	docker rm -f mobsf || true && \
	docker pull opensecurity/mobile-security-framework-mobsf && \
	docker run -d -it -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest --name mobsf
