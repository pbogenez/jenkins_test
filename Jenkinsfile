pipeline {
  agent any
  stages {
    stage('push to git') {
      steps {
        sh '''if [ ! `git branch --list release` ]
   then git branch release
fi

echo "this is some new content" > anewfile.txt
git add *
git commit -m "a new branch"
git push origin main'''
      }
    }

  }
}