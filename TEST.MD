# Virus App : récupération du pays par défaut et envoie des informations dans le back end

Nous avons mis en place un pays par défaut, et non les statistiques du monde entier pour les nombres de cas au lancement de l'application, car étant français nous nous sommes dit que cela allait faire gagner du temps aux utilisateurs.

## Définir le pays par défaut:

Pour qu'à chaque fois que l'on ouvre l'application la France soit par défaut sur le pays choisis, dans la class Covid19 nous avons mis en paramètre 'fr' dans countryCode


``` 
class Covid19 extends React.Component {
    constructor() {
        super();
        this.state = {l
            countries: [],
            stats: {},
            countryCode: 'fr',
            date: '2020-06-18'
        }
    } 
```
 ensuite avec la function getdailybycountry nous allons regarder si l'utilisateur est loggé, puis récupérer les country et la date  ensuite nous allons faire un appel à l'api pour set le country et la date.

``` public function getDailyByCountry(Request $request, AuthenticationService $authenticationService)
    {
        $authorization = $request->headers->get('Authorization');
        $country = $request->query->get('country');
        $date = $request->query->get('date');

```


```
 public function getDailyByCountry(Request $request, AuthenticationService $authenticationService)
    {
        $authorization = $request->headers->get('Authorization');
        $country = $request->query->get('country');
        $date = $request->query->get('date');
        $response = new Response;
        if (isset($payload['userId'])) {
            $client = new \GuzzleHttp\Client();
            $resp = $client->request(
                'GET',
                'https://covid-19-data.p.rapidapi.com/report/country/code?format=json&date-format=YYYY-MM-DD&date=' . $date . '&code=' . $country, [
                "headers" => [
                    "X-RapidAPI-Host" => $_SERVER['API_HOST'],
                    'X-RapidAPI-Key' => $_SERVER['API_KEY']
                ]
            ]);

            $response->headers->set('Content-Type', 'application/json');
            $response->setContent($resp->getBody()->getContents());
            return $response;
        }
        $response->setStatusCode(401);
        return $response;
    }
```