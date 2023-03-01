#клас Обробник
class Handler
  def next_handler=(handler)
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end


  def handle(request)
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end
end


#Організація роботи обробників. Формування ланцюга
class AbstractHandler < Handler
  attr_writer :next_handler

  def next_handler(handler)
    @next_handler = handler
    handler
  end


  def handle(request)
    return @next_handler.handle(request) if @next_handler
    nil
  end
end


#Обробник, що допомагає у питаннях грошей. В іншому випадку - передає запит за ланцюгом
class MoneySpec < AbstractHandler
  def handle(request)
    if request == 'Гроші'
      "Грош_Спеціаліст: Вирішу Ваші питання з - #{request}"
    else
      super(request)
    end
  end
end


#Обробник, що допомагає у питаннях з роутером. В іншому випадку - передає запит за ланцюгом
class RoutSpec < AbstractHandler
  def handle(request)
    if request == 'Роутер'
      "Роут_Спеціаліст: Вирішу Ваші питання з - #{request}"
    else
      super(request)
    end
  end
end


#Обробник, що допомагає у питаннях з сервером. В іншому випадку - передає запит за ланцюгом
class ServerSpec < AbstractHandler
  def handle(request)
    if request == 'Сервер'
      "Сервер_Спеціаліст: Вирішу Ваші питання з - #{request}"
    else
      super(request)
    end
  end
end


#Обробник, що допомагає у питаннях з Інтернетом. В іншому випадку - передає запит за ланцюгом
class InternetSpec < AbstractHandler
  def handle(request)
    if request == 'Інтернет'
      "Інтернет_Спеціаліст: Вирішу Ваші питання з - #{request}"
    else
      super(request)
    end
  end
end


#Послідовність запитів (звернень клієнтів).
def Clients_requests(handler)
  ['Інтернет', 'Гроші', 'Роутер', 'Сервер', 'Гра'].each do |request|
    puts "\nКлієнт: Маю проблеми з: #{request}. Хтось може допомогти?"
    result = handler.handle(request)
    if result
      print "  #{result}"
    else
      print "Проблема #{request} залишилась невирішеною."
    end
  end
end

#Створення обробників.
moneySP = MoneySpec.new
internetSP = InternetSpec.new
serverSP = ServerSpec.new
routeSP =RoutSpec.new


#Задаємо послідовність ланцюга, навмання.
moneySP.next_handler(routeSP).next_handler(internetSP).next_handler(serverSP)


puts 'Ланцюг звернень: Проблема з Інтернетом -> Грошові питання -> Проблема з роутером
-> Проблема з сервером -> Проблема з грою'
puts 'Обробники звернень: ГрошСпец -> ІнтернетСпец -> СерверСпец -> РоутерСпец'
Clients_requests(moneySP)
puts "\n\n"


puts 'Альтернативний вид: виключено ланки лацюга (обробників) ГрошСпец та РоутерСпец'
Clients_requests(internetSP)