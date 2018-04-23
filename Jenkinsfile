pipeline {
	agent {
		label 'master'
}

	options{
		buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))


}
	
	stages{
		stage('Unit Tests'){
			steps {
					sh 'ant -f test.xml -v'
					junit 'reports/result.xml'
}
	

}


		stage('build'){
			steps {
			sh 'ant -f build.xml -v'
			sh 'hostname'
			sh 'pwd'
			sh 'echo $env.BUILD_NUMBER'
}
}
		stage('deploy'){
			steps{
				sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
				sh "pwd"
				
}
		

}
}
	post{
		always{
			archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
}
}

}
