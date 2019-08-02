#!/usr/bin/env groovy

class Image {
    String baseImageName
    String amberImageTag
}

List<Image> dockerImagesToBuild = [
    new Image(baseImageName: "ubuntu/18.04", amberImageTag: "amber/cpu-build:test"),
    new Image(baseImageName: "nvidia/cuda:10.1-devel-ubuntu18.04", amberImageTag: "amber/gpu-build:test")
]

pipeline {

    agent none

    stages {

        stage("Build and push the docker images") {
            when {
                branch "feature/initial"
            }

            steps {
                script {
                    for (dockerImageToBuild in dockerImagesToBuild) {
                        echo "Building ${dockerImageToBuild.amberImageTag} from ${dockerImageToBuild.baseImageName}"
                        def image = docker.build(dockerImageToBuild.amberImageTag, "--build-arg BASE_IMAGE=${dockerImageToBuild.baseImageName}")

                        docker.withRegistry("", "amber-docker-credentials") {
                            echo "Pushing ${dockerImageToBuild.amberImageTag} from ${dockerImageToBuild.baseImageName}"
                            image.push()
                        }
                    }
                }
            }
        }

    }
}
