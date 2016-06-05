node {
  stage 'Stage Checkout'

  checkout scm
  sh 'git submodule update --init'  

  stage 'Stage Build'

  //branch name from Jenkins environment variables
  echo "My branch is: ${env.BRANCH_NAME}"

  def flavor = flavor(env.BRANCH_NAME)
  echo "Building flavor ${flavor}"

  def os = [:]
  os["sid"] = {
    sh "export TRAVIS_DEBIAN_DISTRIBUTION=sid; wget -O- http://travis.debian.net/script.sh | sh -"
  }
  os["jessie"] = {
    sh "export TRAVIS_DEBIAN_DISTRIBUTION=jessie; wget -O- http://travis.debian.net/script.sh | sh -"
  }

  parallel os

  stage 'Stage Archive'
  // tell Jenkins to archive the debs
  // ..

  stage 'Stage Upload'
  // ...
}

@NonCPS
def flavor(branchName) {
  def matcher = (env.BRANCH_NAME =~ /([a-z_]+)/)
  assert matcher.matches()
  matcher[0][1]
}
