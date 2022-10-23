

# Extend blueprint editor menu Window Layout example

The module FBlueprintEditorModule must be loaded on post engine initialization. The editor will crash at launch if trying to load before.



```
void FMyModule::StartupModule()
{
    //Standard plugin code....

    FDelegateHandle CoreDelegateHand = FCoreDelegate::OnPostEngineInit.AddRaw(this, &FMyModule::OnPostEngineInit);
}

void FMyModule::OnPostEngineInit()
{
	FBlueprintEditorModule& BlueprintEditorModule = FModuleManager::LoadModuleChecked<FBlueprintEditorModule>("Kismet");
	{
		TSharedPtr<FExtender> BPMenuExtender = MakeShareable(new FExtender());
		BPMenuExtender->AddMenuExtension("WindowLayout", EExtensionHook::After, PluginCommands, FMenuExtensionDelegate::CreateRaw(this, &FSimpleNotesModule::AddMenuExtension));

		BlueprintEditorModule.GetMenuExtensibilityManager()->AddExtender(BPMenuExtender);
    }
}
```

Blueprint Editor result:
