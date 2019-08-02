#!/usr/bin/env groovy

class Image {
    String dockerfileFolder
    String baseImageName
    String amberImageTag
}

List<Image> dockerImagesToBuild = [
    new Image(dockerfileFolder: 'debian-based',
              baseImageName: "ubuntu:18.04",
              amberImageTag: "ambermd/cpu-build:latest"),

    new Image(dockerfileFolder: 'debian-based',
              baseImageName: "nvidia/cuda:10.1-devel-ubuntu18.04",
              amberImageTag: "ambermd/gpu-build:latest")
]

pipeline {

    agent none

    stages {

        stage("Build and push the docker images") {
            agent {
                label 'docker'
            }

            when {
                branch "master"
            }

            steps {
                script {
                    for (dockerImageToBuild in dockerImagesToBuild) {
                        String imageTag = dockerImageToBuild.amberImageTag
                        String baseImage = dockerImageToBuild.baseImageName
                        String folder = dockerImageToBuild.dockerfileFolder

                        echo "Building ${imageTag} from ${baseImage}"
                        def image = docker.build(imageTag, "--build-arg BASEIMAGE=${baseImage} ${folder}")

                        docker.withRegistry("", "amber-docker-credentials") {
                            echo "Pushing ${imageTag} from ${baseImage}"
                            image.push()
                        }
                    }
                }
            }
        }

    }
}
