#!/usr/bin/env groovy

class Image {
    String dockerfileFolder
    String baseImageName
    String amberImageTag
}

List<Image> dockerImagesToBuild = [
    new Image(dockerfileFolder: 'debian-based',
              baseImageName: "ubuntu:18.04",
              amberImageTag: "ambermd/cpu-build"),

    new Image(dockerfileFolder: 'debian-based',
              baseImageName: "nvidia/cuda:10.1-devel-ubuntu18.04",
              amberImageTag: "ambermd/gpu-build"),

    new Image(dockerfileFolder: "gcc-based",
              baseImageName: "gcc:9.1.0",
              amberImageTag: "ambermd/gcc91-build"),

    new Image(dockerfileFolder: "cuda-opencl",
              baseImageName: "nvidia/cuda:10.1-devel-ubuntu18.04",
              amberImageTag: "swails/openmm-all"),
]

pipeline {

    agent none

    stages {

        stage("Build and push the docker images") {
            agent {
                label 'docker'
            }

            steps {
                script {
                    String tagName = "test"
                    if (env.GIT_BRANCH == "master") {
                        tagName = "latest"
                    }
                    for (dockerImageToBuild in dockerImagesToBuild) {
                        String imageTag = dockerImageToBuild.amberImageTag + ":" + tagName
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
