"use client"

import { useState, useEffect } from "react"
import Image from "next/image"
import Link from "next/link"
import { Menu, X } from "lucide-react"

import { cn } from "@/lib/utils"

export default function Home() {
  const [menuOpen, setMenuOpen] = useState(false)
  const [activeProject, setActiveProject] = useState(0)
  const [isLoaded, setIsLoaded] = useState(false)

  useEffect(() => {
    setIsLoaded(true)
  }, [])

  const projects = [
    {
      id: 1,
      title: "주택 프로젝트",
      category: "주거",
      location: "서울",
      year: "2023",
      image: "/placeholder.svg?height=800&width=1200",
    },
    {
      id: 2,
      title: "오피스 빌딩",
      category: "상업",
      location: "부산",
      year: "2022",
      image: "/placeholder.svg?height=800&width=1200",
    },
    {
      id: 3,
      title: "갤러리 공간",
      category: "문화",
      location: "제주",
      year: "2021",
      image: "/placeholder.svg?height=800&width=1200",
    },
    {
      id: 4,
      title: "카페 인테리어",
      category: "상업",
      location: "서울",
      year: "2023",
      image: "/placeholder.svg?height=800&width=1200",
    },
  ]

  return (
    <div
      className={cn(
        "min-h-screen bg-white text-black transition-opacity duration-1000",
        isLoaded ? "opacity-100" : "opacity-0",
      )}
    >
      {/* Mobile menu */}
      <div
        className={cn(
          "fixed inset-0 z-50 flex flex-col bg-white p-6 transition-transform duration-300",
          menuOpen ? "translate-x-0" : "translate-x-full",
        )}
      >
        <button
          onClick={() => setMenuOpen(false)}
          className="absolute right-6 top-6 text-black"
          aria-label="Close menu"
        >
          <X className="h-6 w-6" />
        </button>
        <div className="mt-20 flex flex-col space-y-6 text-lg">
          <Link href="#projects" className="hover:opacity-50" onClick={() => setMenuOpen(false)}>
            PROJECTS
          </Link>
          <Link href="#about" className="hover:opacity-50" onClick={() => setMenuOpen(false)}>
            ABOUT
          </Link>
          <Link href="#contact" className="hover:opacity-50" onClick={() => setMenuOpen(false)}>
            CONTACT
          </Link>
        </div>
      </div>

      {/* Header */}
      <header className="fixed top-0 z-40 w-full bg-white py-6">
        <div className="mx-auto flex items-center justify-between px-6 md:px-12">
          <div className="text-xl font-light tracking-widest">
            <Link href="/">EL DREAM</Link>
          </div>
          <nav className="hidden md:flex gap-10">
            <Link href="#projects" className="text-sm tracking-wider hover:opacity-50">
              PROJECTS
            </Link>
            <Link href="#about" className="text-sm tracking-wider hover:opacity-50">
              ABOUT
            </Link>
            <Link href="#contact" className="text-sm tracking-wider hover:opacity-50">
              CONTACT
            </Link>
          </nav>
          <button onClick={() => setMenuOpen(true)} className="z-50 block md:hidden" aria-label="Open menu">
            <Menu className="h-6 w-6" />
          </button>
        </div>
      </header>

      <main>
        {/* Hero Section */}
        <section className="h-screen w-full pt-24">
          <div className="h-full w-full">
            <div className="grid h-full grid-cols-1 md:grid-cols-2">
              <div className="flex flex-col items-start justify-center p-6 md:p-12">
                <h1 className="text-3xl font-light tracking-wider md:text-4xl">EL DREAM</h1>
                <p className="mt-4 text-sm font-light tracking-wide md:text-base">건축 설계 사무소</p>
              </div>
              <div className="relative hidden h-full md:block">
                <Image
                  src="/placeholder.svg?height=1080&width=1080"
                  alt="건축 공간"
                  fill
                  className="object-cover"
                  priority
                />
              </div>
            </div>
          </div>
        </section>

        {/* Projects Section */}
        <section id="projects" className="py-24">
          <div className="mx-auto px-6 md:px-12">
            <h2 className="mb-12 text-sm font-light tracking-widest">PROJECTS</h2>

            <div className="grid gap-6 md:grid-cols-2">
              <div className="order-2 md:order-1">
                <div className="sticky top-24 space-y-6">
                  {projects.map((project, index) => (
                    <div
                      key={project.id}
                      className={cn(
                        "cursor-pointer py-2 transition-opacity duration-300",
                        activeProject === index ? "opacity-100" : "opacity-50",
                      )}
                      onMouseEnter={() => setActiveProject(index)}
                    >
                      <h3 className="text-lg font-light">{project.title}</h3>
                      <div className="mt-1 flex gap-4 text-xs font-light">
                        <span>{project.category}</span>
                        <span>{project.location}</span>
                        <span>{project.year}</span>
                      </div>
                    </div>
                  ))}
                </div>
              </div>

              <div className="order-1 md:order-2">
                <div className="relative aspect-[4/3] w-full overflow-hidden">
                  {projects.map((project, index) => (
                    <div
                      key={project.id}
                      className={cn(
                        "absolute inset-0 transition-opacity duration-500",
                        activeProject === index ? "opacity-100" : "opacity-0",
                      )}
                    >
                      <Image
                        src={project.image || "/placeholder.svg"}
                        alt={project.title}
                        fill
                        className="object-cover"
                      />
                    </div>
                  ))}
                </div>
              </div>
            </div>
          </div>
        </section>

        {/* About Section */}
        <section id="about" className="py-24">
          <div className="mx-auto px-6 md:px-12">
            <h2 className="mb-12 text-sm font-light tracking-widest">ABOUT</h2>
            <div className="grid gap-12 md:grid-cols-2">
              <div>
                <p className="text-sm font-light leading-relaxed">
                  EL DREAM은 건축 시공과 디자인 분야에서 혁신적인 솔루션을 제공합니다. 우리는 공간의 기능성과 미학적
                  가치를 균형 있게 조화시키는 것을 목표로 합니다.
                </p>
                <p className="mt-6 text-sm font-light leading-relaxed">
                  전문적인 시공 기술과 창의적인 디자인을 통해 고객의 비전을 실현합니다.
                </p>
              </div>
              <div>
                <p className="text-sm font-light leading-relaxed">
                  2005년 설립된 이래로, 우리는 다양한 규모와 유형의 프로젝트를 성공적으로 완료했습니다. 주거, 상업, 문화
                  공간 등 다양한 분야에서 우리만의 독특한 접근 방식으로 공간의 가치를 높이는 건축을 추구합니다.
                </p>
              </div>
            </div>

            <div className="mt-24 grid gap-6 md:grid-cols-3">
              <div>
                <h3 className="mb-2 text-sm font-light tracking-widest">SERVICES</h3>
                <ul className="space-y-1 text-sm font-light">
                  <li>건축 설계</li>
                  <li>인테리어 디자인</li>
                  <li>건축 시공</li>
                  <li>리모델링</li>
                  <li>건축 컨설팅</li>
                </ul>
              </div>
              <div>
                <h3 className="mb-2 text-sm font-light tracking-widest">TEAM</h3>
                <ul className="space-y-1 text-sm font-light">
                  <li>건축가 5명</li>
                  <li>인테리어 디자이너 3명</li>
                  <li>시공 전문가 7명</li>
                  <li>프로젝트 매니저 2명</li>
                </ul>
              </div>
              <div>
                <h3 className="mb-2 text-sm font-light tracking-widest">AWARDS</h3>
                <ul className="space-y-1 text-sm font-light">
                  <li>2023 한국건축문화대상</li>
                  <li>2022 굿디자인 어워드</li>
                  <li>2020 서울시 건축상</li>
                  <li>2018 대한민국 공간디자인 대상</li>
                </ul>
              </div>
            </div>
          </div>
        </section>

        {/* Contact Section */}
        <section id="contact" className="py-24">
          <div className="mx-auto px-6 md:px-12">
            <h2 className="mb-12 text-sm font-light tracking-widest">CONTACT</h2>
            <div className="grid gap-12 md:grid-cols-2">
              <div>
                <div className="mb-6">
                  <h3 className="mb-2 text-sm font-light tracking-widest">ADDRESS</h3>
                  <p className="text-sm font-light">서울특별시 강남구 테헤란로 123, EL DREAM</p>
                </div>
                <div className="mb-6">
                  <h3 className="mb-2 text-sm font-light tracking-widest">PHONE</h3>
                  <p className="text-sm font-light">+82 02-123-4567</p>
                </div>
                <div>
                  <h3 className="mb-2 text-sm font-light tracking-widest">EMAIL</h3>
                  <p className="text-sm font-light">info@eldream.kr</p>
                </div>
              </div>
              <div>
                <form className="space-y-6">
                  <div>
                    <input
                      id="name"
                      className="w-full border-b border-black/20 bg-transparent py-2 text-sm font-light focus:border-black focus:outline-none"
                      placeholder="NAME"
                    />
                  </div>
                  <div>
                    <input
                      id="email"
                      type="email"
                      className="w-full border-b border-black/20 bg-transparent py-2 text-sm font-light focus:border-black focus:outline-none"
                      placeholder="EMAIL"
                    />
                  </div>
                  <div>
                    <textarea
                      id="message"
                      className="h-32 w-full border-b border-black/20 bg-transparent py-2 text-sm font-light focus:border-black focus:outline-none"
                      placeholder="MESSAGE"
                    />
                  </div>
                  <button className="text-sm font-light tracking-widest hover:opacity-50">SEND</button>
                </form>
              </div>
            </div>
          </div>
        </section>
      </main>

      {/* Footer */}
      <footer className="border-t border-black/10 py-6">
        <div className="mx-auto px-6 md:px-12">
          <div className="flex flex-col items-center justify-between gap-4 md:flex-row">
            <div className="text-xs font-light">© 2023 EL DREAM. All rights reserved.</div>
            <div className="flex gap-6">
              <Link href="#" className="text-xs font-light hover:opacity-50">
                INSTAGRAM
              </Link>
              <Link href="#" className="text-xs font-light hover:opacity-50">
                FACEBOOK
              </Link>
              <Link href="#" className="text-xs font-light hover:opacity-50">
                PINTEREST
              </Link>
            </div>
          </div>
        </div>
      </footer>
    </div>
  )
}
