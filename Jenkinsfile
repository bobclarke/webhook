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

	if( result.ref ){
		println "This is either a push, merge or a tag event, let's find out which"
		def type = result.ref.split('/')[1]
		println "\nTYPE :" + type
		if( type.toLowerCase().contains('head')){
			println "it's a push or a merge, same thing"
			return "push"
		}
	}
}
