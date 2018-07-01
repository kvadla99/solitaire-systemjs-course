stage 'Integration'
node {
    checkout scm
    //git branch: 'jenkins2-course',
    //    url: 'https://github.com/santom11/solitaire-systemjs-course.git'

    sh 'npm install'
    
    stash name: 'everything'
          excludes: 'test-result/**'
          includes: '**'

    sh 'npm run test-single-run -- --browsers PhantomJS'
       
        
    step([$class: 'JUnitResultArchiver', testResults: 'test-results/**/test-results.xml'])

    
}

node {
    stage 'Deploy to test env ?'
}   

input 'Deploy to test env?'

stage name: 'Deploy', concurrency: 1
node {
    sh 'docker-compose up -d --build'
}
