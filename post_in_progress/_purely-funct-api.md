---
layout:       post
title:        "Trip to purely functional API - Part I"
description:  "Structuring app and selecting technologies"
category:     articles
tags:         [fp, functional programming, type classes, scala, monads, effects, cats, mtl, monad, environmental effects]
---

Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.


```scala
object AccountController extends Controller {

  def routes[F[_]: Sync]: HttpRoutes[F] = {

    val dsl = new Http4sDsl[F] {}
    import dsl._

    HttpRoutes.of[F] {
      case req @ POST -> Root / ACCOUNTS =>
        for {
          accountRequest <- req.as[AccountRequest]
          account        <- AccountApplicationService.open[F](accountRequest)
          resp           <- Ok(account)
        } yield resp
      case req @ POST -> Root / ACCOUNTS / TRANSFER =>
        for {
          transferRequest <- req.as[TransferRequest]
          result          <- AccountApplicationService.transfer[F](transferRequest)
          resp            <- Ok(result)
        } yield resp
    }
  }
}
```

Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a


Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a


```scala
trait AccountService[F[_]] {
  def open(no: String, name: String, email: String, rate: Option[BigDecimal], accountType: AccountType): F[Account]
  def close(no: String, closeDate: Date): F[Account]
  def debit(no: String, amount: Amount): F[Account]
  def credit(no: String, amount: Amount): F[Account]
  def transfer(from: String, to: String, amount: Amount)(implicit M: Monad[F]): F[(Account, Account)] =
    for {
      a <- debit(from, amount)
      b <- credit(to, amount)
    } yield (a, b)
}

object AccountService {
  def apply[F[_]](implicit F: AccountService[F]): AccountService[F] = F
}
```