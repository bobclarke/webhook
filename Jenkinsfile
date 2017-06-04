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
		stage( "uploadArtifact" ) {
			def slurper = new groovy.json.JsonSlurperClassic()
			def reader = new BufferedReader(new InputStreamReader(new FileInputStream("package.json"),"UTF-8"));
			data = jsonSlurper.parse(reader);       
			def tag = data.version
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



