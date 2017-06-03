//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Setup
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
import groovy.json.JsonSlurperClassic 

println "\nPAYLOAD: "+ env.payload +"\n"


//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// main
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
def eventType = getEventType( payload )
switch (eventType) {
	case "push": println "\nEVENTTYPE " +eventType; break;
	case "pull": println "\nEVENTTYPE " +eventType; break;
	case "tag": println "\nEVENTTYPE " +eventType; break;
	default: println "Something else";
}


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

	if( result.pull_request  && result.action.toLowerCase().contains("opened") ){
		return "pull"
	}

	else if( result.ref && result.head_commit){

		if( result.ref.split('/')[1].toLowerCase().contains('head') ){
			return "push"
		}

		else if( result.ref.split('/')[1].toLowerCase().contains('tag') ){
			return "tag"
		}
	}
}

