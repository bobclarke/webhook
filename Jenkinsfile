//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Setup
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
import groovy.json.JsonSlurperClassic 

println "\nPAYLOAD: "+ env.payload +"\n"


//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// main
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

checkout()

def eventType = getEventType( payload )
switch (eventType) {
	case "push": 
		build( eventType ); 
		build( "Test" ); 
		uploadArtifact();
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

private void checkout(){
	node {
		stage( "Checkout" ) {
			checkout scm
		}
	}
}

private void uploadArtifact(){
	node {
		stage( "uploadArtifact" ){
			env.WORKSPACE = pwd()
			def json = readFile "${env.WORKSPACE}/package.json"
			def slurper = new groovy.json.JsonSlurperClassic()
			data = slurper.parseText( json );       
			def tag = data.version
			def props = readJSON file: 'package.json'
			println "TAG: " +tag
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



