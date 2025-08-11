tasks.register("Push") {
  dependsOn('lwjgl3:packageLinuxX64', 'lwjgl3:packageWinX64')

  doLast {
    println "Pushing builds to itch.io..."

    // Replace with your itch.io username and game slug
    def userGame = "zrm9901/random-dice-game"
    def name = project.subprojects.find { it.name == 'lwjgl3' }?.ext?.appName
    def lin = "${project(':lwjgl3').buildDir}\\construo\\dist\\${name}-linuxX64.zip"
    def win = "${project(':lwjgl3').buildDir}\\construo\\dist\\${name}-winX64.zip"

    exec {
      commandLine "butler", "push", lin, "$userGame:Linux"
    }
    exec {
      commandLine "butler", "push", win, "$userGame:Windows"
    }
  }
}
