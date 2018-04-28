pipeline {
	agent none

	options{
		buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))


}
	
	stages{
	
		stage('Unit Tests'){
			 agent{
	                        label 'apache'
}

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

			        post{
                			success{
                        			archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
}
}

}
		stage('deploy'){
			agent{
				label 'apache'
}
			steps{
				sh "mkdir -p /var/www/html/rectangles/all/${env.BRANCH_NAME}"
				sh "cp dist/rectangle_${BUILD_NUMBER}.jar /var/www/html/rectangles/all/${env.BRANCH_NAME}/"
				sh "pwd"
				
}
		

}

		stage("Testing on CentOS"){
			agent{
				label 'CentOS'
}
		steps{
			sh "wget http://172.31.26.211/rectangles/all/${env.BRANCH_NAME}/rectangle_${BUILD_NUMBER}.jar"
			sh "java -jar rectangle_${BUILD_NUMBER}.jar 3 4"
}

}
		stage("Testing on Debian"){
			agent{
				docker 'openjdk:8u121-jre'
}
			steps{
				sh "wget http://172.31.26.211/rectangles/all/${env.BRANCH_NAME}/rectangle_${BUILD_NUMBER}.jar"
                        sh "java -jar rectangle_${BUILD_NUMBER}.jar 3 4"

}
}

		stage("Promote to green folder in apache"){

			agent {
				label 'apache'
}

			when{
				branch 'master'
}
			steps{
				sh "cp /var/www/html/rectangles/all/${env.BRANCH_NAME}/rectangle_${BUILD_NUMBER}.jar /var/www/html/rectangles/green/"
}

}

		stage("promote development branch to master"){

			agent{
				label 'apache'
}

			when{
				branch 'development'
}

			steps{

				echo "stashing Any Local Changes"
				sh 'git stash'
				echo "Checking Out Development Branch"
				sh 'git checkout development'
				echo 'Checking Out Master Brance'
				sh 'git checkout master'
				echo "Merging Development into Master Branch"

				sh 'git merge development'
				echo 'Pushing to Origin Master'
				sh 'git push origin master'

				echo "amer4"
}
}



}
	

}

