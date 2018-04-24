pipeline {
	agent none

	options{
		buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))


}
	
	stages{
		agent{
			label 'apache'
}
		stage('Unit Tests'){
			steps {
					sh 'ant -f test.xml -v'
					junit 'reports/result.xml'
}
	

}


		stage('build'){
			agent{
				label 'apache'
}
			steps {
			sh 'ant -f build.xml -v'
			sh 'hostname'
			sh 'pwd'
			sh 'echo $BUILD_NUMBER'
}
}
		stage('deploy'){
			agent{
				label 'apache'
}
			steps{
				sh "cp dist/rectangle_${BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
				sh "pwd"
				
}
		

}

		stage("Testing on CentOS"){
			agent{
				label 'CentOS'
}
		steps{
			sh "wget http://172.31.26.211/rectangles/all/rectangle_${BUILD_NUMBER}.jar"
			sh "java -jar rectangle_${BUILD_NUMBER}.jar 3 4"
}

}

}
	post{
		always{
			archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
}
}

}

