TabView 的实现

实现1 
``` swift
import SwiftUI

private struct Tab: View {
    let imageName: String
    let text: String
    
    var body: some View {
        VStack {
            Image(systemName: imageName)
            Text(text)
        }
    }
}

struct ContentView: View {
    var body: some View {
        TabView {
            StatsView()
                .tabItem {
                    Tab(imageName: "chart.bar", text: "stats")
            }
            .tag(0)
            
            ContainerMapView()
                .edgesIgnoringSafeArea(.vertical)
                .tabItem {
                    Tab(imageName: "map", text: "Maps")
            }
            .tag(1)
            
            AdviceView()
                .tabItem {
                    Tab(imageName: "tray.full", text: "Advices")
            }
            .tag(2)
            
            AboutView()
                .tabItem {
                    Tab(imageName: "person", text: "About")
            }
            .tag(3)
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
            .environment(\.colorScheme, .dark)
    }
}
```

实现2
``` swift

import SwiftUI

struct RootView: View {
    @State private var selection: Int = 0
    
    var body: some View {
        NavigationView {
            TabView(selection: $selection) {
                ChatHome()
                    .tabItem { Item(type: .chat, selection: selection) }
                    .tag(ItemType.chat.rawValue)
                ContactHome()
                    .tabItem { Item(type: .contact, selection: selection) }
                    .tag(ItemType.contact.rawValue)
                DiscoverHome()
                    .tabItem { Item(type: .discover, selection: selection) }
                    .tag(ItemType.discover.rawValue)
                MeHome()
                    .tabItem { Item(type: .me, selection: selection) }
                    .tag(ItemType.me.rawValue)
            }
            .navigationBarHidden(itemType.isNavigationBarHidden(selection: selection))
            .navigationBarTitle(itemType.title, displayMode: .inline)
            .navigationBarItems(trailing: itemType.navigationBarTrailingItems(selection: selection))
        }
    }
    
    enum ItemType: Int {
        case chat
        case contact
        case discover
        case me
        
        var image: Image {
            switch self {
            case .chat:     return Image("root_tab_chat")
            case .contact:  return Image("root_tab_contact")
            case .discover: return Image("root_tab_discover")
            case .me:       return Image("root_tab_me")
            }
        }
        
        var selectedImage: Image {
            switch self {
            case .chat:     return Image("root_tab_chat_selected")
            case .contact:  return Image("root_tab_contact_selected")
            case .discover: return Image("root_tab_discover_selected")
            case .me:       return Image("root_tab_me_selected")
            }
        }
        
        var title: String {
            switch self {
            case .chat:     return "微信"
            case .contact:  return "通讯录"
            case .discover: return "发现"
            case .me:       return "我"
            }
        }
        
        func isNavigationBarHidden(selection: Int) -> Bool {
            selection == ItemType.me.rawValue
        }
        
        func navigationBarTrailingItems(selection: Int) -> AnyView {
            switch ItemType(rawValue: selection)! {
            case .chat:
                return AnyView(Image(systemName: "plus.circle"))
            case .contact:
                return AnyView(Image(systemName: "person.badge.plus"))
            case .discover:
                return AnyView(EmptyView())
            case .me:
                return AnyView(EmptyView())
            }
        }
    }
    
    struct Item: View {
        let type: ItemType
        let selection: Int
        
        var body: some View {
            VStack {
                if type.rawValue == selection {
                    type.selectedImage
                } else {
                    type.image
                }
                
                Text(type.title)
            }
        }
    }
    
    private var itemType: ItemType { ItemType(rawValue: selection)! }
}

struct RootTabView_Previews : PreviewProvider {
    static var previews: some View {
        RootView()
    }
}

```

实现3

``` swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        TabView {
            DashboardTabView()
                .tabItem {
                    VStack {
                        Text("Dashboard")
                        Image(systemName: "chart.pie")
                    }
            }
            .tag(0)
            
            LogsTabView()
                .tabItem {
                    VStack {
                        Text("Logs")
                        Image(systemName: "tray")
                    }
            }
            .tag(1)
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

```

实现4
```swift

import SwiftUI

extension Color {
    var rgb: String { "\(self)".capitalized }
}

struct ContentView: View {

    var body: some View {
        TabView {
            InfiniteExampleView()
                .tabItem({
                    Image(systemName: "goforward")
                    Text("Infinite")
                }).tag(0)
            ColorsExampleView()
                .tabItem({
                    Image(systemName: "forward.fill")
                    Text("Manual")
                }).tag(1)
            EmbeddedExampleView()
                .tabItem({
                    Image(systemName: "flowchart.fill")
                    Text("In ScrollView")
                }).tag(2)
            NestedExampleView()
                .tabItem({
                    Image(systemName: "rectangle.on.rectangle")
                    Text("Nested")
                }).tag(3)
            BizarreExampleView()
                .tabItem({
                    Image(systemName: "smiley")
                    Text("Bizarre")
                }).tag(4)
        }
    }

}

```

实现5
```swift

struct TabViews: View {
    
    @ObservedObject var settingsViewModel: SettingsViewModel
    @ObservedObject var passwordListViewModel: PasswordListViewModel
    @ObservedObject var passwordGeneratorViewModel:PasswordGeneratorViewModel
    
    var body: some View {
        
        VStack {
            TabView(content: {
                        
                        PasswordGeneratorView(settings: settingsViewModel,
                                              passwordViewModel: passwordListViewModel)
    
                            .tabItem {
                                
                                Label(title: { Text("Générateur") },
                                      icon: { Image(systemName: "die.face.5.fill") })
                                
                            }.tag(0)
                        
                        PasswordListView(passwordViewModel: passwordListViewModel,
                                         settings: settingsViewModel,
                                         passwordGeneratorViewModel: passwordGeneratorViewModel, settingsViewModel: settingsViewModel)
            
                            .tabItem {
                    
                                Label(title: { Text("Coffre fort") },
                                      icon: { Image(systemName: "lock.square") })
                                
                                
                            }.tag(1)
                        
                        SettingsView(settingsViewModel: settingsViewModel,
                                     biometricType: settingsViewModel.biometricType(),
                                     passwordViewModel: passwordListViewModel )
                
                            .tabItem {
                                
                                Label(title: { Text("Préférences") },
                                      icon: { Image(systemName: "gear") })
                                       .animation(.easeIn)
                                
                            }.tag(2) })
            
        }
    }
}

struct TabViews_Previews: PreviewProvider {
    static var previews: some View {
        TabViews(settingsViewModel: SettingsViewModel(), passwordListViewModel: PasswordListViewModel(), passwordGeneratorViewModel: PasswordGeneratorViewModel())
    }
}

```

实现6
```swift
import SwiftUI

struct TabedView : View {
    private let context = CoreDataManager.shared.managedObjectContext
    
    var body: some View {
        TabView {
            MainView()
                .tabItem {
                    Image(systemName: "globe")
                        .font(.system(size: 22))
                }
            
            SourcesListView()
                .tabItem {
                    Image(systemName: "list.bullet")
                        .font(.system(size: 22))
                }
            
            SearchForArticlesView()
                .tabItem {
                    Image(systemName: "magnifyingglass")
                        .font(.system(size: 22))
                }
            
            FavoritesView()
                .environment(\.managedObjectContext, context)
                .tabItem {
                    Image(systemName: "heart.fill")
                        .font(.system(size: 22))
                }
            
            WeatherView()
                .tabItem {
                    Image(systemName: "cloud.sun.fill")
                        .font(.system(size: 22))
                }
        }
        .accentColor(.black)
    }
}

```

实现6
```swift
  private var tabBarView: some View {
    TabView(selection: .init(get: {
      selectedTab
    }, set: { newTab in
      if newTab == selectedTab {
        /// Stupid hack to trigger onChange binding in tab views.
        popToRootTab = .other
        DispatchQueue.main.asyncAfter(deadline: .now() + 0.01) {
          popToRootTab = selectedTab
        }
      }

      HapticManager.shared.fireHaptic(of: .tabSelection)
      SoundEffectManager.shared.playSound(of: .tabSelection)

      selectedTab = newTab

      DispatchQueue.main.async {
        if selectedTab == .notifications,
           let token = appAccountsManager.currentAccount.oauthToken
        {
          userPreferences.setNotification(count: 0, token: token)
          watcher.unreadNotificationsCount = 0
        }
      }

    })) {
      ForEach(availableTabs) { tab in
        tab.makeContentView(popToRootTab: $popToRootTab)
          .tabItem {
            if userPreferences.showiPhoneTabLabel {
              tab.label
                .labelStyle(TitleAndIconLabelStyle())
            } else {
              tab.label
                .labelStyle(IconOnlyLabelStyle())
            }
          }
          .tag(tab)
          .badge(badgeFor(tab: tab))
          .toolbarBackground(theme.primaryBackgroundColor.opacity(0.50), for: .tabBar)
      }
    }
    .id(appAccountsManager.currentClient.id)
  }

  private func setNewClientsInEnv(client: Client) {
    currentAccount.setClient(client: client)
    currentInstance.setClient(client: client)
    userPreferences.setClient(client: client)
    Task {
      await currentInstance.fetchCurrentInstance()
      watcher.setClient(client: client, instanceStreamingURL: currentInstance.instance?.urls?.streamingApi)
      watcher.watch(streams: [.user, .direct])
    }
  }

  private func handleScenePhase(scenePhase: ScenePhase) {
    switch scenePhase {
    case .background:
      watcher.stopWatching()
    case .active:
      watcher.watch(streams: [.user, .direct])
      UIApplication.shared.applicationIconBadgeNumber = 0
      Task {
        await userPreferences.refreshServerPreferences()
      }
    default:
      break
    }
  }

  private func setupRevenueCat() {
    Purchases.logLevel = .error
    Purchases.configure(withAPIKey: "appl_JXmiRckOzXXTsHKitQiicXCvMQi")
    Purchases.shared.getCustomerInfo { info, _ in
      if info?.entitlements["Supporter"]?.isActive == true {
        isSupporter = true
      }
    }
  }

  private func refreshPushSubs() {
    PushNotificationsService.shared.requestPushNotifications()
  }

  @CommandsBuilder
  private var appMenu: some Commands {
    CommandGroup(replacing: .newItem) {
      Button("menu.new-post") {
        sidebarRouterPath.presentedSheet = .newStatusEditor(visibility: userPreferences.postVisibility)
      }
    }
    CommandGroup(replacing: .textFormatting) {
      Menu("menu.font") {
        Button("menu.font.bigger") {
          if theme.fontSizeScale < 1.5 {
            theme.fontSizeScale += 0.1
          }
        }
        Button("menu.font.smaller") {
          if theme.fontSizeScale > 0.5 {
            theme.fontSizeScale -= 0.1
          }
        }
      }
    }
  }
}
```
