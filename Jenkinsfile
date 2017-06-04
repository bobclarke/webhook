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
	case "push": 
		build( eventType ); 
		build( "Test" ); 
		break;
	case "pull": 
		build( eventType ); 
		break;
	default: 
		println "Something else";
}


//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// subs
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
private void build( eventType ){
	node {
		stage( eventType ) {
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

