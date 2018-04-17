pipeline {
	agent any

	options{
		buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))


}
	
	stages{
		stage('build'){
			steps {
			sh 'ant -f build.xml -v'
			sh 'hostname'
			sh 'pwd'
}
}
}
	post{
		always{
			archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
}
}

}
