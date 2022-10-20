# itz-Badsha-
It's badsha
<html>

<head>

    <meta charset="UTF-8">

    <title>OKSDK - REST notifications.sendSimple (nosession)</title>

    <script type="text/javascript" src="../oksdk.js"></script>

</head>

<body>

<div id="content" style="display: none;">

    <p>

        WARNING: This is just a sample (of REST method calling without active session using OKSDK).

        In real game, storing application secret key inside your JS client app is prohibited due to

        easy way to steal it and use for spamming purposes. Such methods should only be called from

        game server instead.

        <br/>

        <input type="button" onclick="sendSimple();" value="Send simple message"/><br/>

        Posts a simple "hello world!" notification

    </p>

</div>

<script type="text/javascript">

    var currentUserUID = 0;

    function sendSimple() {

        OKSDK.REST.call("notifications.sendSimple",

                {uid: currentUserUID, text: 'Hello world from oksdk.js!'},

                function (status, data, error) {

                    if (status == 'ok') {

                        alert('SendSimple sent ok: ' + OKSDK.Util.toString(data));

                    } else {

                        alert('Error with send simple to user ' + currentUserUID + ': ' + OKSDK.Util.toString(error));

                    }

                },

                {no_session: true, app_secret_key: '' /* <-- insert APP SECRET KEY here */}

        );

    }

    document.addEventListener('DOMContentLoaded', function () {

        var config = {

            app_id: 0,      // <-- insert APP ID here

            app_key: ''     // <-- insert APP PUBLIC KEY here

        };

        OKSDK.init(config, function () {

            document.getElementById('content').style.display = '';

            OKSDK.REST.call("users.getCurrentUser",

                    {fields: "UID"},

                    function (status, data, error) {

                        if (status == 'ok') {

                            currentUserUID = data.uid;

                        } else {

                            alert('Error with retrieving current user ' + OKSDK.Util.toString(error));

                        }

                    });

        }, function (error) {

            alert('OKSDK error' + OKSDK.Util.toString(error));

        })

    });

</script>

</body>

</html>
