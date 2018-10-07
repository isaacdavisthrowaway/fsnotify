
This is a test of force-pushing to a PR

node {
	stage 'build' {
		node('go1.11-build') {
    		echo '11'

		}
		node('go1.10-build') {
    		echo '10'
		}
		node('go1.9-build') {
			echo '9'			
		}
		node('go1.8-build') {
			echo '8'
		}
	}
}
