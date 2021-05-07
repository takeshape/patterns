# Magic Trick

The schema that lets you (virtually) pull a rabbit out of your hat.

<a href="https://app.takeshape.io/add-to-takeshape?repo=https://github.com/takeshape/patterns/tree/main/magic-trick"><img alt="Deploy To TakeShape" src="https://camo.githubusercontent.com/1b580e3ce353d235bde0f376ca35b0fb26d685f3750a3013ae4b225dd3aaf344/68747470733a2f2f696d616765732e74616b6573686170652e696f2f32636363633832352d373062652d343331632d396261302d3130616233386563643361372f6465762f38653266376264612d306530382d346564652d613534362d3664663539626536613862622f4465706c6f79253230746f25323054616b65536861706525343032782e706e673f6175746f3d666f726d6174253243636f6d7072657373" width="205" height="38" data-canonical-src="https://images.takeshape.io/2cccc825-70be-431c-9ba0-10ab38ecd3a7/dev/8e2f7bda-0e08-4ede-a546-6df59be6a8bb/Deploy%20to%20TakeShape%402x.png?auto=format%2Ccompress" style="max-width:100%;"></a>

## APIs

- [Twilio](https://www.twilio.com/docs/sms/api)
- [PetFinder](https://www.petfinder.com/developers/v2/docs/)

## Usage

1. Set up a Twilio account on Twilio and add your credentials and personal endpoint to the service provided by this pattern in the TakeShape UI. The endpoint will appear in your Twilio account and look something like this: `https://api.twilio.com/2010-04-01/Accounts/ACcc8cb2cb9c1a99f454926ed7e7f09e01`
2. Set up a Petfinder account on Petfinder and add your credentials to the service provided by this pattern in the TakeShape UI.
3. In Twilio, approve the phone number you want to use for the `to` input in `checkSleeve` above.
4. Use your Twilio assigned phone number for the `from` input above.
5. Run the query below in the TakeShape API explorer with those two phone numbers substituted. You should receive a text at the `to` number with a rabbit.

## Story

This schema makes use of TakeShape's ability to pipe and manipulate data between APIs
solely relying on configuration. Here we take a phone number as input, access the
Petfinder API with a query scoped to `rabbits`, and form this up into a message
we send via SMS to the number provided.

## Query

```graphql
mutation MagicTrick {
  checkSleeve(phone: "+17817758338") {
    bunny {
      name
      description
      age
      gender
      size
    }
    message {
      from
      to
      status
    }
  }
}
```
