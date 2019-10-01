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

    new Image(dockerfileFolder: "openmm-cpu",
              baseImageName: "ubuntu:18.04",
              amberImageTag: "swails/openmm-cpu"),

    new Image(dockerfileFolder: "lyx",
              baseImageName: "ubuntu:18.04",
              amberImageTag: "ambermd/lyx"),
]

pipeline {

    agent none

    options {
        skipDefaultCheckout()
    }

    stages {

        stage("Checkout and stash build") {
            agent {
                label 'linux'
            }

            steps {
                dir("common-dockerfiles") {
                    checkout scm
                }

                stash includes: '**', name: 'source', useDefaultExcludes: false
            }

            post { cleanup { deleteDir() } }
        }

        stage("Build and push the docker images") {
            agent {
                label 'docker'
            }

            steps {
                unstash 'source'
                dir('common-dockerfiles') {
                    script {
                        String tagName = "test"
                        echo "env.BRANCH_NAME = ${env.BRANCH_NAME}"
                        if ("${env.BRANCH_NAME}" == "master") {
                            echo "Running on master branch, using 'latest' tag"
                            tagName = "latest"
                        }
                        for (dockerImageToBuild in dockerImagesToBuild) {
                            String imageTag = dockerImageToBuild.amberImageTag + ":" + tagName
                            String baseImage = dockerImageToBuild.baseImageName
                            String folder = dockerImageToBuild.dockerfileFolder

                            def image = docker.build(imageTag, "--build-arg BASEIMAGE=${baseImage} ${folder}")

                            docker.withRegistry("", "amber-docker-credentials") {
                                echo "Pushing ${imageTag} from ${baseImage}"
                                image.push()
                            }
                        }
                    }
                }
            }

            post { cleanup { deleteDir() } }
        }
    }
}
