pipeline {
	agent any
	
	stages{
		stage('build'){
			steps {
			sh 'ant -f build.xml -v'
			sh 'hostname'
}
}
}
	post{
		always{
			archive 'dist/*.jar'
}
}

}
