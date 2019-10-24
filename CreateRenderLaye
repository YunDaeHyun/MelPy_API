import sys
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx
import maya.cmds as cmds

kPluginCmdName = "AutoLayering"

# Command
class scriptedCommand(OpenMayaMPx.MPxCommand):
    def __init__(self):
        OpenMayaMPx.MPxCommand.__init__(self)
        
    # Invoked when the command is run.
    def doIt(self,argList):

        st = cmds.ls(sl=1)
        cmds.createRenderLayer(st)
        cmds.vray("objectProperties","add_single")
        cmds.editRenderLayerGlobals(currentRenderLayer="renderLayer")
        cmds.setAttr("vrayobjectproperties.primaryVisibility",0)
        cmds.editRenderLayerAdjustment("vrayobjectproperties.primaryVisibility")
        cmds.setAttr("vrayobjectproperties.primaryVisibility",1)
        cmds.rename("renderLayer",str(st)) 
        cmds.rename("vrayobjectproperties",str(st)) 
    

# Creator
def cmdCreator():
    return OpenMayaMPx.asMPxPtr( scriptedCommand() )
    
# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.registerCommand( kPluginCmdName, cmdCreator )
    except:
        sys.stderr.write( "Failed to register command: %s\n" % kPluginCmdName )
        raise

# Uninitialize the script plug-in
def uninitializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand( kPluginCmdName )
    except:
        sys.stderr.write( "Failed to unregister command: %s\n" % kPluginCmdName )
