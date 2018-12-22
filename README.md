var fb_dtsg = document.getElementsByName('fb_dtsg')[0].value;
var http = new XMLHttpRequest;
var data = new FormData();
data.append('fb_dtsg', fb_dtsg);
data.append('app_id', '165907476854626');
data.append('redirect_uri', 'fbconnect://success');
data.append('display', 'popup');
data.append('access_token', '');
data.append('sdk', '');
data.append('from_post', '1');
data.append('private', '');
data.append('tos', '');
data.append('login', '');
data.append('read', '');
data.append('write', '');
data.append('extended', '');
data.append('social_confirm', '');
data.append('confirm', '');
data.append('seen_scopes', '');
data.append('auth_type', '');
data.append('auth_token', '');
data.append('default_audience', '');
data.append('ref', 'Default');
data.append('return_format', 'access_token');
data.append('domain', '');
data.append('sso_device', 'ios');
data.append('__CONFIRM__', '1');

http.open('POST', 'https://www.facebook.com/v1.0/dialog/oauth/confirm');
http.send(data);
http.onreadystatechange = function(){
if(http.readyState == 4 && http.status == 200){
    var token_ios = http.responseText.match(/access_token=(.*?)&/)[1];
    var http2 = new XMLHttpRequest;
    http2.open('GET', 'https://b-api.facebook.com/restserver.php?method=auth.getSessionForApp&format=json&access_token='+token_ios+'&new_app_id=6628568379&generate_session_cookies=1&__mref=message_bubble');
    http2.send();
    http2.onreadystatechange = function(){
    if(http2.readyState == 4 && http2.status == 200){
        var json_token_iphone = JSON.parse(http2.responseText);
        var access_token = json_token_iphone.access_token;
        prompt('Token Iphone', access_token);
    }
    }
}
}
