# How to use the WaveGuardAPI

### First get the instances from our Main-Class

````java
public class WaveGuardTest extends JavaPlugin {

    private static WaveGuardTest instance;

    private final WaveGuard waveguard = WaveGuard.getInstance();
    private final ConfigManager configManager = waveguard.getConfigManager();
    private final IWaveGuardAPI iWaveGuardAPI = waveguard.getIWaveGuardAPI();

    private final FloodgateHook floodgateHook = waveguard.getFloodgateHook();
    private final IVersionHelper iVersionHelper = waveguard.getIVersionHelper();
    private final WebhookClient webhookClient = waveguard.getWebhookClient();

    private final ChannelHandler channelHandler = waveguard.getChannelHandler();
    private final CrashCheckHandler crashCheckHandler = waveguard.getCrashCheckHandler();
    private final BotCheckHandler botCheckHandler = waveguard.getBotCheckHandler();

    public void onEnable() {
        instance = this;
    }

    public void onDisable() {

    }


    public IWaveGuardAPI getIWaveGuardAPI() {
        return iWaveGuardAPI;
    }

    public ConfigManager getConfigManager() {
        return configManager;
    }

    public FloodgateHook getFloodgateHook() {
        return floodgateHook;
    }

    public IVersionHelper getIVersionHelper() {
        return iVersionHelper;
    }

    public WebhookClient getWebhookClient() {
        return webhookClient;
    }

    public ChannelHandler getChannelHandler() {
        return channelHandler;
    }

    public CrashCheckHandler getCrashCheckHandler() {
        return crashCheckHandler;
    }

    public BotCheckHandler getBotCheckHandler() {
        return botCheckHandler;
    }


    public static WaveGuardTest getInstance() {
        return instance;
    }
}
````

<br>

---

### How to check a VPN

````java
public class CheckVPN implements Listener {

    private final WaveGuardTest waveguardTest = WaveGuardTest.getInstance();
    private final IWaveGuardAPI iWaveGuardAPI = waveguardTest.getIWaveGuardAPI();
    private final ConfigManager configManager = waveguardTest.getConfigManager();

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent event) {
        HashMap<HashMapKeys, JsonElement> checkedProxy = this.iWaveGuardAPI.checkProxy("IP to check", "license" ->
        (this.configManager.getConfig(Config.LICENSE, ID.LICENSE.getId()), "HWID" ->(Licensing.getHWID())));

        final boolean isProxy = !checkedProxy.get(HashMapKeys.PROXY).isJsonNull() && checkedProxy.get(HashMapKeys.PROXY).getAsBoolean();

        if (isProxy) {
            System.out.println("IP is a VPN");
        } else {
            System.out.prinln("IP is not a VPN");
        }
    }
}
````
