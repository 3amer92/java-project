pipeline {
	agent any
	
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
