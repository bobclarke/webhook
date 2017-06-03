//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Setup
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
import groovy.json.JsonSlurperClassic 

println "\nPAYLOAD: "+ env.payload +"\n"


//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// main
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
build()
def eventType = getEventType( payload )
println "\nEVENTTYPE " +eventType

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// subs
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
private void build(){
	node {
		stage('Build') {
			echo 'Building....'
		}
	}
}

private String getEventType ( payload ){

	def slurper = new groovy.json.JsonSlurperClassic()
	def result = slurper.parseText( payload )

	if( result.pull_request ){
		return "pull"
	}

	else if( result.ref && result.head_commit){
		if( result.ref.split('/')[1].toLowerCase().contains('head')){
			return "push"
		}
	}
}

