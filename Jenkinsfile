pipeline {

     agent {
        docker {
          image 'drobovictor/dz11prep'
          //arguments for mapping sockets and user root
          args '-v /var/run/docker.sock:/var/run/docker.sock -u 0:0'
          //authenthication on dockerHUB
          registryCredentialsId 'a8775578-df81-4cf1-8deb-5ba31b4fd211'
          }
        }

        stages {

          stage('copying wedapp repo') {
             steps {
             //копируем репозиторий с тестовым приложением
             //предварительно подкидываем в него докерфайл для создания продового образа
             git 'https://github.com/Sandenev/boxfusefortest'
             }
          }
          stage('building war file') {
             steps {
                sh 'mvn package'
             }
          }
          stage('build and push docker image to dockerHUB') {
            steps {
              sh 'docker build -f Dockerfile -t drobovictor/dz11prod .'
              sh 'docker push drobovictor/dz11prod'
            }
          }
        }
     }